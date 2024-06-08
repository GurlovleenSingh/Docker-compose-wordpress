# Wordpress deployment with Docker Compose

## Description

Project focused on Docker Compose file for deploying WordPress. 
This Compose file will include WordPress itself, along with a MySQL database container.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

Docker Engine: Docker is a containerization platform that allows you to package and run applications and their dependencies in isolated containers. You'll need Docker Engine installed on the host machine where you plan to deploy WordPress. You can install Docker Engine by following the official Docker documentation specific to your operating system: Install Docker Engine.

Docker Compose: Docker Compose is a tool for defining and running multi-container Docker applications. It uses YAML files to configure the application's services, networks, and volumes. Docker Compose is typically included with Docker Engine on most platforms. However, if it's not installed, you can follow the instructions in the official Docker documentation: Install Docker Compose.

WordPress Docker Image: Docker images are used to create Docker containers. You'll need the WordPress Docker image, which contains the WordPress application and its dependencies. You can pull the official WordPress image from Docker Hub using the following command:
docker pull wordpress:latest


MySQL Docker Image: WordPress requires a MySQL database to store its data. You'll also need the MySQL Docker image. You can pull the official MySQL image from Docker Hub using the following command:
docker pull mysql:5.7

## Usage
Step by step guide:
1. Create a directory: First, create a directory for your project:
mkdir wordpress-docker
cd wordpress-docker
2. create a dockercompose file: docker Composefile is written in YAML language. its extenstion will be .yml.
Create a file named docker-compose.yml in your project directory. code is below. Make ENV chnages as required.

version: '3.7'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_mysql_root_password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: your_mysql_password

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: your_mysql_password
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data:

2. Save the docker-compose.yml file and then run the following command in your terminal:
docker-compose up -d

3.Access WordPress: Once the containers are up and running, you can access WordPress by opening your web browser and navigating to http://localhost:8000

4. To stop the containers use thefollowing command.
docker-compose down
The command will stop and remove the containers defined in your docker-compose.yml file. 
If you also want to remove volumes associated with the containers, you can add the -v option:
docker-compose down -v


## Credits
 Visual studio, dockerhub
