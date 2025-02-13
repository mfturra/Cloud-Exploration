# Launching Apache Ubuntu Server on AWS EC2 T2 Micro Instance
1. Configure and launch the AWS Cloud hardware server (i.e. Ubuntu OS server)
2. SSH into it and take the following steps to configure your Apache server.

## Requirements
Ubuntu server has already been stood up.
Apache build is for a Ubuntu 20.04 or 22.04 server.
User has a fundamental understanding how to build a Flask app using Python.

### Install Apache Server
#### Background
An Apache server is a web server that’s responsible for handling client requests via the browser. As the user interacts with the browser, Apache listens to the requests then sends the respective web-pages back to the clients browser.

* Update the local package list: `sudo apt-get update`
* Update any outdated packages: `sudo apt-get upgrade`
* Install the apache2 package onto your server, while bypassing need to submit yes as part of config steps: `sudo apt install apache2 -y`
* Enable and start the Apache server: `sudo systemctl enable apache2 && sudo systemctl start apache2`

#### Apache Verification & Troubleshooting
Proceed with the following steps to ensure that Apache is running correctly.

Method #1: Utilize the system’s init system to ensure that the service is running appropriately.
* Evaluate Apache server status: `sudo systemctl status apache2`
* Expected output should include a detailed list of content regarding your Apache HTTP server.

Method #2: Navigate to the Apache landing page to confirm that the server is running properly through your IP Address.
* Identify Respective IP Address(es): `hostname -I`
* Enter IP address into browser
* Expected output is the Ubuntu 20.04 Apache web page.

### Install Python Dependencies
* Install Python3, pip, and Python’s venv: `sudo apt-get install python3 python3-pip python3-venv`
* Verify that Python was successfully installed by acquiring your Python version: `python3 -V`
* Output should be some variation of the following: 
`root@host:~# python3 -V`
`Python 3.10.4`
* Create a directory where respective Flask app documents will be copied: `mkdir app-name`
* Change into that working directory: `cd app-name`
* Create a Python venv in your files directory to install Flask dependencies: `python3 -m venv flask-venv`
* Activate the virtual Flask environment: `source flask-venv activate`
* Command prompt will change to the following
    * Original: `root@host:/home/app-name#`
    * New venv: `(flask-venv) root@host:/home/app-name#`
* Install Flask in the venv: `pip3 install flask`

### Creating/Copying Respective Flask App Files
Method 1: Copy GitHub repo into directory
* Copy and paste the GitHub repo URL into the terminal and press enter.
* All respective documents will now be downloaded by the Ubuntu server

Method 2: Create files from scratch
* Create a sample Flask app using a Python file: `sudo nano app.py`
* While inside the file, paste the respective Flask script to test its usage. Save and close the file.
* Setup the FLASK_APP environment variable by inserting the following in the CLI: `export FLASK_APP=app.py`
* Run the Flask app: `flask run`

### Create WSGI file for VENV
**Background (Reference)**
A _Web Server Gateway Interface (WSGI)_ works as the specification that describes how a web server should communicate with a Python web app or framework (i.e. Flask). In order to utilize it, the WSGI server needs to be installed onto the Apache server. mod_wsgi is one of many other WSGI servers. It’s a Python package that works as an Apache module that creates a compliant interface for hosting Python-based web apps on an Apache server.
* Install mod_wsgi to allow Flask app to interact with Apache server: `sudo apt-get install libapache2-mod-wsgi-py3`
* Create the WSGI file: `sudo nano /home/app-name/flask-app.wsgi`
* Once inside the file, paste the following lines of code then save and close the file:
```
import sys
sys.path.insert(0, ‘home/app-name’)
from app import app as application
```

Create Apache Virtual Host File
Background (Reference)
A domain or individual site is also known as a Virtual Host. It dictates how a client will access a specific directory that holds the information of interest. Virtual host files are the files that specify the actual configuration of our virtual hosts and dictate how the Apache web server responds to a client’s various domain requests. 

Create the flask virtual host file: touch /etc/apache2/sites-available/flask.conf
Insert the following lines then save and close the file:
```
<VirtualHost *:80>
ServerName yourdomain.com
DocumentRoot /home/app-name/

WSGIDaemonProcess app user=www-data group=www-data threads=5 python-home=/home/app-name/flask-venv
WSGIScriptAlias / /home/app-name/flask-app.wsgi

ErrorLog ${APACHE_LOG_DIR}/flask-error.log
CustomLog ${APACHE_LOG_DIR}/flask-access.log combined

<Directory /opt/flask-app>
WSGIProcessGroup app
WSGIApplicationGroup %{GLOBAL}
Order deny,allow
Require all granted
</Directory>
</VirtualHost>
```
Enable the Apache2 config file: `sudo a2ensite flask.conf`
Evaluate the syntax of the Apache2 configuration: `apachectl -t`
Expected output: 
```
    root@host:~# apachectl -t
    Syntax OK
```
If the previous output is received, restart the Apache service: `sudo systemctl restart apache2`

### Command Line Prompts
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt install apache2 -y`
4. `sudo systemctl enable apache2 && sudo systemctl start apache2`
5. `sudo apt-get install python3 python3-pip python3-venv`
6. `mkdir /home/app-name`

### Create a separate Apache directory for a specific user
1. `cd app-name`
2. `python3 -m venv flask-venv`
3. `source flask-venv activate`
4. `pip3 install flask`
5. `git clone https://github.com/mfturra/media-backlog-api.git`
6. `sudo apt-get install libapache2-mod-wsgi-py3`
7. `sudo nano /home/app-name/flask-app.wsgi`
8. `touch /etc/apache2/sites-available/flask.conf`
9. `cd /etc/apache2/sites-available`
10. `sudo nano flask.conf.`
11. `sudo a2ensite flask.conf`
12. `apachectl -t`
13. `sudo systemctl restart apache2`    

Troubleshooting Steps for Enabling an Apache Server
* `sudo systemctl status apache2`
* `hostname -I`

Running Flask app: `flask run`
