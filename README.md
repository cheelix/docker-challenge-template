# docker-challenge-template

Install docker
 
1 Update the software package index:
sudo apt-get update
2 Install necessary packages to allow apt to use repositories over HTTPS:
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
3 Add Docker's official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
4 Add Docker's stable repository:
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
5 Update the software package index to ensure access to the Docker repository packages:
sudo apt-get update
6 Install Docker CE (Community Edition):
sudo apt-get install docker-ce
7 Install Docker Compose:
wget https://github.com/docker/compose/releases/download/v2.26.1/docker-compose-linux-x86_64
mv docker-compose-linux-x86_64 /usr/local/bin
sudo chmod +x /usr/local/bin/docker-compose
8 Check the installed versions of Docker and Docker Compose.

 
 



Challenge3

1  Create .env and docker-compose.yaml files.  
2 Set the database username, password, and the name of the initial database in the .env file.
 
3 Use docker-compose.yaml to orchestrate containers.
version: '3'
services:
  nginx:
    build:
      context: ./nginx
      dockerfile: Dockerfile
    ports:
      - 8080:80
    depends_on:
      - node-service

  node-service:
    build:
      context: ./api
      dockerfile: Dockerfile
    ports:
      - 3000
    depends_on:
      - db
    environment:
      - DB_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
      - DB_DATABASE=${DB_DATABASE}
      - DB_USERNAME=${DB_USERNAME}
      - DB_PASSWORD=${DB_PASSWORD}
      - DB_HOST=${DB_HOST}


  db:
    build:
      context: ./db
      dockerfile: Dockerfile
    environment:
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
      - MYSQL_DATABASE=${MYSQL_DATABASE}
      - MYSQL_USER=${MYSQL_USER}
      - MYSQL_PASSWORD=${MYSQL_PASSWORD}
      - MYSQL_HOST=${MYSQL_HOST}
4 Build the image and start the container.
 

 



5  View http://localhost:8080/api/books 

 
6 View  http://localhost:8080/api/books/1
 

7	Run 'docker-compose ps' to view the containers that have been started.  


challenge4

1 Use the application from challenge3 to view http://localhost:8080/api/stats. 
 
2  Scale up.
 
3 Accessing http://localhost:8080/api/stats multiple times, I noticed that the hostname changes
 
 
4 Run 'docker-compose ps' to check.
 
