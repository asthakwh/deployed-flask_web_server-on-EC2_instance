# deployed-flask_web_server-on-EC2_instance

python3 -v
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

pip install gunicorn
gunicorn -b 0.0.0.0:8000 app:app


