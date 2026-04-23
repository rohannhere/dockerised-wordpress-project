# dockerised-wordpress-project
Containerized WordPress on AWS EC2

🚀 Dockerized WordPress Setup on AWS EC2
📌 Project Overview

This project demonstrates how to deploy a WordPress web application using Docker containers on an AWS EC2 instance.

Instead of following the traditional and lengthy LAMP stack setup, this approach uses Docker to quickly spin up:

A MySQL database container
A WordPress application container

Both containers are linked together for seamless communication.

🧩 Tech Stack
Docker
WordPress
MySQL
AWS EC2

⚙️ Step-by-Step Setup

1️⃣ Launch EC2 Instance
Create an EC2 instance (Amazon Linux recommended)
Connect using SSH

2️⃣ Install Docker
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker

(Optional: Run Docker without sudo)
sudo usermod -aG docker ec2-user

3️⃣ Create MySQL Container
docker run -d --name mydb \
-e MYSQL_ROOT_PASSWORD=<your_pass> \
-e MYSQL_DATABASE=wordpressdb \
mysql

🔍 Explanation:
-d → Run container in detached mode (background)
--name mydb → Assigns container name
MYSQL_ROOT_PASSWORD → Sets root password for MySQL
MYSQL_DATABASE → Creates a database named wordpressdb
mysql → Official MySQL image

4️⃣ Create WordPress Container
docker run -d -P --name myWordpress \
-e WORDPRESS_DB_HOST=mydb \
-e WORDPRESS_DB_USER=root \
-e WORDPRESS_DB_PASSWORD=<your_pass> \
-e WORDPRESS_DB_NAME=wordpressdb \
--link mydb:mysql \
wordpress

🔍 Explanation:
-d → Run in background
-P → Automatically map container ports to random host ports
--name myWordpress → Container name
WORDPRESS_DB_HOST=mydb → Connects to MySQL container
WORDPRESS_DB_USER=root → MySQL username
WORDPRESS_DB_PASSWORD → MySQL password
WORDPRESS_DB_NAME → Database name
--link mydb:mysql → Links WordPress container to MySQL container
wordpress → Official WordPress image

🔄 Verify Running Containers
docker ps

You should see both:
mydb
myWordpress

🌐 Access WordPress
Copy your EC2 Public IP
Get port from:
docker ps

Open in browser:
http://<your-ec2-public-ip>:<port>
Example:
http://12.56.4.110:32772

⚠️ Troubleshooting
❌ Site not reachable?
Check your EC2 Security Group:
  Allow inbound traffic on:
  Port 80 (HTTP)
  Or your mapped port (e.g., 32772)

🤝 Contributing
Feel free to fork this repo and experiment!


