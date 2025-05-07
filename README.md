# scored_task_docker

This is a docker compose file that builds a fastapi application with postgre as database, redis as cache directory, and nginx as reverse proxy web server.

## file structure
/fastapi_app\
│  ├── app/ \
│  │    └── main.py\
│  ├── requirements.txt\
│  ├── Dockerfile\
│  └── docker-compose.yml\
│\
└── nginx/\
     └── nginx.conf


## FastAPI app
This app is designed to take notes from user, save it in database sequentially, and print them out using the database id 
It's written with python and using FastAPI for the backend communications 
its container is built on on the python alpine image for smaller size and quicker deployment

## NGINX as reverse proxy 
All web traffic is managed by NGINX to listen to requests and redirect them to the suitable instance
It's built on an alpine image with NGINX added and configuration file with suitable path inside the image itself

## PostgreSQL database
The database that holds all the notes taken in the app.

## Redis cache
The cached database is a quicker link to the app itself, quicker response from the app in as long as the container is running, as it's deleted after shutdown 

## Docker images justification 
### 1- Python FastAPI app
The app is built on the python alpine image to minimize vulnerability, increase deployment speed, and increase reliability 

### 2- NGINX
Instead of using the official nginx alpine image, i started with an alpine base image which then NGINX was installed onto with the needed paths and configuration file
The image is <10MB in size versus the offical 28MB image

### 3- Postgre DB
Using the bitnami image the Postgre image is smaller than the official image -105MB vs 155MB- and no vulnerabilities

### 4- Redis
The official redis alpine had no vulnerablities and was lightweight so it didn't need any alteration 