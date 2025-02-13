# Objective
Deploy AWS Instance and connect it to a Flask API.

[Reference](https://medium.com/techfront/step-by-step-visual-guide-on-deploying-a-flask-application-on-aws-ec2-8e3e8b82c4f7 )

## Steps to Deployment
* Change directory to the folder where the key pair is located
* Secure the key pairs by running the following script: `chmod 400 vs-flask-1.cer`
* Run the following scripts to connect to the EC2 server: `ssh -i "vs-flask-1.cer" ubuntu@ec2-123456.us-east-2.compute.amazonaws.com`
  - Where:
      - `vs-flask-1.cer` is the key pair name in quotations.
      - `ubuntu@ec2-123456.us-east-2.compute.amazonaws.com` is the cloud location of the server instance.

### If dependencies haven't been installed yet:
- Install Python Virtualenv
  - `sudo apt-get update`
  - `sudo apt-get install python3-venv`

### Activate virtual environment
1. Create directory
    - `mkdir media-backlog-api`
    - `cd media-backlog-api`
2. Create new virtual environment
    - `python3 -m venv venv`
3. Activate the virtual environment
    - `source venv/bin/activate`
4. Install Flask
    - `pip install Flask`
    - `pip install flask_sqlalchemy`
    - `sudo apt install libpq-dev` (Facilitates psycopg2 install on Ubuntu)
    - `pip install psycopg2-binary` This is a drop-in replacement to psycopg2 that eliminates the need for building from source.

### Create basic Flask API
- Open app.py file: `sudo nano app.py`
- Paste app.py script in file.
- Paste the following after sqlalchemy library import.
  - `from sqlalchemy.ext.declarative import declarative_base`
- Define Base and paste Videogame Class after app config section.
  - `Base = declarative_base()`
- Select `Ctrl + O`. Save file by selecting Enter.
- Exit nano by selecting `Ctrl + X`
- Verify that the file is as it should be by pasting the following: `cat app.py`
- Test that the app's running: `python app.py`

## Run Gunicorn WSGI server to connect Flask Application
1. Install Gunicorn 
    - `pip install gunicorn`
2. Run Gunicorn
    - `gunicorn -b 0.0.0.0:8000 app:app`
    - Exit using: Ctl + C
