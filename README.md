# Cloud-Exploration
Industries have transitioned many of their local services to the Cloud. This repository represents the knowledge base that I accumulated over a couple of years as I explored deploying AWS Cloud instances and connected them to local ports via Flask APIs.

### 🚀 Concepts Explored (AWS Cloud & PostgreSQL Database)
* Configure Apache Ubuntu Server on AWS EC2 T2 micro instance with necessary Python dependencies to run a basic Flask app on it.
* Building RDS PostgreSQL database on AWS EC2 T2 micro instance with the following configs:
    * Storage: General Purpose SSD (gp2), 20GB of space, autoscaling disabled.
    * Connectivity: Default VPC, Subnet, and Security groups
    * Database Authentication: Password
* Stand up AWS Instance and deploy a Flask app on the server
   * Install & activate Python virtual env
   * Create a basix Flask API
   * Install & run Gunicorn to connect to Flask app.
* Build VideoGame Database
     * Install Postgres and Flask-SQLAlchemy to connect a Flask app to the database
     * Utilize CURL to submit an HTTP GET & POST request with JSON data to a local server.
     * Create Videogame class (e.g. gameName, gamePlatform, releaseDate) & store in database with a unique UUID.
