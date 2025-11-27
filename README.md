# aws-ec2-rds-project
A cloud-based deployment using AWS EC2 as the application server and AWS RDS as the managed database, showcasing secure connectivity, database operations, and core cloud infrastructure setup.

AWS RDS + EC2 Project
Cloud-Hosted Application using AWS EC2 & RDS

This project demonstrates how to deploy a cloud-based application using an EC2 instance connected to an RDS MySQL/PostgreSQL database.
It follows a production-style architecture where compute and database layers are separated for better security, performance, and scalability.

Project Overview

The goal of this project is to host an application on an EC2 instance and connect it to a managed relational database on AWS RDS.
This setup replicates how modern applications run in real-world environments.

Architecture:

                       +-----------------------------+
                       |           USER              |
                       +--------------+--------------+
                                      |
                                      v
                               Internet Access
                                      |
                                      v
                       +--------------+--------------+
                       |         AWS EC2 Instance    |
                       |   (App Code + DB Client)    |
                       +--------------+--------------+
                                      |
                               Security Group Rules
                                      |
                                      v
                       +--------------+--------------+
                       |          AWS RDS            |
                       |   (Managed SQL Database)    |
                       +------------------------------+

Technologies Used:
AWS EC2
AWS RDS (MySQL/PostgreSQL)
Linux (Ubuntu)
Security Groups
SSH
Basic SQL Commands

Setup Instructions:
1️⃣ Create an RDS Database

Go to AWS Console → RDS → Create Database
Choose:
Engine: MySQL or PostgreSQL
Template: Free-tier

Set:
DB name
Master username
Master password

Select:
Public access: YES (for development only)
Security group: create or choose one that allows inbound 3306 (MySQL) or 5432 (PostgreSQL)
Wait for database to finish creating.


2️⃣ Create an EC2 Instance
Go to EC2 → Launch Instance
Choose:
AMI: Ubuntu 22.04
Instance type: t2.micro

Add key pair for SSH access

Configure security group:
Allow SSH (22) from your IP
Allow HTTP (80) if deploying a web app

Launch the instance.


3️⃣ SSH Into the EC2 Instance
ssh -i "your-key.pem" ubuntu@<EC2-Public-IP>

4️⃣ Install MySQL/PostgreSQL Client on EC2

For MySQL:
sudo apt update
sudo apt install mysql-client -y

5️⃣ Connect to RDS from EC2:
mysql -h <RDS-ENDPOINT> -u <username> -p

6️⃣ Run SQL Queries:
CREATE DATABASE aws;
USE aws;
CREATE TABLE learners(learner_id INT PRIMARY KEY, learner_name VARCHAR(50));
INSERT INTO learners VALUES(1, "Aditi");
SELECT * FROM users;

Security Notes:
Never leave RDS public in production.
Use VPC + private subnets.
Configure least-privilege access.

Conclusion:<img width="1366" height="662" alt="rds" src="https://github.com/user-attachments/assets/ba684eac-c17a-4b79-9917-6fa61e9c0e9e" />

This project gives hands-on experience in:
Cloud deployment
Server–database connectivity
Networking & security
Basic Linux server management
