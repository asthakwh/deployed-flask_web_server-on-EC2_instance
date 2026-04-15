# deployed-flask_web_server-on-EC2_instance
python3 -v

mkdir hello

cd hello

sudo nano app.py


#######################
from flask import Flask

app = Flask(__name__)

@app.route('/')

def hello_world():

	return 'hellow world!@'
	
if __name__ == "__main__":

	app.run()
##########################

source venv/bin/activate

pip install flask

pip install gunicorn

gunicorn -b 0.0.0.0:8000 app:app

now create a file with "sudo nano /etc/systemd/system/hello.service"
############################
[Unit]

Description= Gunicorn instance for a simple hello app

After=network.target

[Service]

User=ubuntu

Group=www-data

WorkingDirectory=/home/ubuntu/hello

ExecStart=/home/ubuntu/hello/venv/bin/gunicorn -b localhost:8000 app:app

Restart=always

[Install]

WantedBy=multi-user.target
##############################

sudo systemctl daemon-reload

sudo systemctl start hello

sudo systemctl enable hello

sudo systemctl status hello

curl localhost:8000

sudo apt install nginx

sudo systemctl start nginx

sudo systemctl enable nginx

sudo systemctl status nginx

sudo nano /etc/nginx/sites-available/default 
###################################
###also enter this on nginx file####
upstream flaskhello {

	server 127.0.0.1:8000;
	
}
####and in below location path remove entry of 404! and add this with your .service file like my filename is hello.service####

location / {

		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		
		proxy_pass http://flaskhello;
		
	}
###################################


sudo systemctl restart nginx

check in browser with IP

Bonus tip: Check that venv is available under hello or your main folder
