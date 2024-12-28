# DOCUMENTATION

# INSTANCE IP: 34.244.67.156

# Server Setup Guide

## Project Overview
This guide outlines the steps to provision a server, set up a web server, and confirm successful installation using AWS EC2 and Nginx.

---

## Step 1: Provisioning the Server

### Choose a Cloud Platform
- **AWS (Amazon Web Services)** is used for this project.
- Sign in to your AWS account or create one if you don’t have an account yet.

### Launch an EC2 Instance
1. Navigate to the **EC2 Dashboard** in AWS.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-23%20215721.png)
2. Click **Launch Instance**.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20021617.png)
3. Configure the instance:
   - Specify the name of the instance
   - **Amazon Machine Image (AMI):** Select an AMI, e.g., Ubuntu Server 20.04 LTS.
   - **Instance Type:** Choose `t2.micro` (AWS Free Tier eligible).
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20021703.png)
4. Set up the **Key Pair:**
   - Specify a key pair name, key pair type as **RSA**, and private key file format as **.pem**.
   - When done creating the key pair, the `.pem` file will be downloaded to your local machine. **NOTE:** This `.pem` file should be kept safe in your local machine. Without it, you won't be able to gain access to your instance.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20021751.png)
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20023929.png)
5. Configure the **Security Group:**
   - Allow SSH traffic from `Anywhere` or your IP (helps you connect to your instance).
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20021823.png)
6. Configure **Storage:**
   - Leave the default storage size (8GB).
7. Launch the instance.
   - The instance will take a few minutes to initialize.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20024644.png)

### Connect to the Server
1. Open a terminal or SSH client (e.g., Termius).
2. Change directory (cd) to the working directory where the `.pem` file is located. Without this file, connection to the instance will be unsuccessful.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20030344.png)
4. Use the following command to connect to the instance:
   ```bash
   ssh -i "your-key-file.pem" ubuntu@<your-instance-public-ip>
   ```
   Replace `your-key-file.pem` with the path to your private key file and `<your-instance-public-ip>` with the instance’s public IP address.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20030414.png)
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20030521.png)
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20030543.png)

---

## Step 2: Web Server Setup

### Prerequisite
Ensure the system is up-to-date.

1. **Update the System:**
   Update the instance using the command `sudo apt update` to ensure the instance is up-to-date. **Note:** I used `sudo` in the command because it's the Ubuntu user and not the root user.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-22%20043036.png)

3. **Install Nginx:**
   Use the command `sudo apt install nginx` to install nginx. Nginx is the software service which renders the web contents or page.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-24%20084910.png)

5. **Start the Nginx Service:**
   Use the command `sudo systemctl start nginx` to activate nginx.

6. **Verify Nginx is Running:**
   Use command `sudo service nginx status` to confirm nginx is active (running).
   Ensure the output shows `active (running)`.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-24%20085131.png)
   
8. **Check Installation:**
   To confirm the above process is working properly, search the instance Public IP Address in a browser (e.g., `34.244.67.156` or `http://34.244.67.156`). You should see the default Nginx welcome page.
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-24%20091306.png)
   
---

## Step 3: Create and Deploy the HTML Page

1. HTML page is displayed via the `/var/www/html/` directory. In this directory, I created a new HTML file to be displayed containing bio of me.
2. In `/var/www/html/` directory, create HTML file using this code
   ```bash
     touch index.html
   ```
3. Use **VIM editor** to edit the new HTML file. Command:
   ```bash
     sudo vi index.html
   ```
4. Image content of index.html
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-28%20130542.png)
5. Replace the default web page in `/var/www/html/` with a new extension. This is done to allow the new HTML file to display properly
   ```bash
     sudo mv index.nginx-debian.html.html index.nginx-debian.html.css
   ```
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-28%20131404.png)

---

## Step 4: Networking Configuration
Security group of the instance is essential to grant access to the instance.
To set up the security group of the instance for HTTP traffic port 80:
1. Navigate to **Network and security**
2. Click **Security Groups**
   ![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-28%20160208.png)
3. Select the security group of the instance
4. Via the **Inbound rule section**, click on **Edit inbound rule**
5. Add rule which states Type `HTTP` Port range `80` Source `Custom` `0.0.0.0/0` This grant access from anywhere in the internet.
   ![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-28%20155228.png)

---

## Final outcome when the IP address of the server is searched on a internet. `IP ADDRESS: 34.244.67.156`
![Alt Text](https://github.com/almightydeus/sec-sem-exam-project/blob/main/Screenshot%202024-12-28%20131909.png)

# INSTANCE IP: 34.244.67.156
