# AWS EC2 Web Server Setup Guide

📌 Objective
- This guide provides a step-by-step approach to launching an Amazon EC2 instance and configuring an Apache Web Server using a user data script. The goal is to deploy a simple, publicly accessible web server on AWS.
---

### 🔹 Prerequisites
- An active AWS account
- Basic knowledge of Linux commands
- An SSH client
- Linux/macOS: Terminal
- Windows: PuTTY or OpenSSH
- A modern web browser
---

## 1️⃣ Launch an EC2 Instance
- Log in to the AWS Management Console
- Search for EC2 and open the EC2 Dashboard
- Click Launch Instance
### Step 2: Configure Instance
- Name and Tags: My Web Server
- Operating System: Amazon Linux 2 (recommended)
- Instance Type: Default (e.g., t2.micro for free tier)
### Step 3: Key Pair Configuration
- Select Create new key pair
- Key pair name: mywebserver-key
- Key pair type: RSA
- Download the .pem file

### ⚠️ Important:
Store the key pair securely. Without it, SSH access to the instance is not possible.

- Step 4: Network Settings
- Allow SSH (Port 22) from your IP address
- Allow HTTP (Port 80) from anywhere (0.0.0.0/0)
- Storage: Default settings or as per requirement
- Step 5: User Data Script
- In Advanced details → User data, paste the following script:
```
#!/bin/bash
sudo yum update -y

# Install Apache web server
sudo yum install -y httpd

# Start Apache service
sudo systemctl start httpd

# Enable Apache on boot
sudo systemctl enable httpd

# Create a simple HTML page
echo "<html>
<h1>Welcome to Apache Web Server on Amazon Linux!</h1>
</html>" | sudo tee /var/www/html/index.html
```

- Click Launch Instance.
---

## 2️⃣ Verify EC2 Instance and Web Server
- Go to EC2 → Instances
- Select the instance named My Web Server
- Copy the Public IPv4 Address
- Paste the IP address into a web browser

- ✅ If Apache is running correctly, the welcome page will load in the browser.
---

## 3️⃣ Security Group Verification
- Select the EC2 instance
- Open the Security tab
- Click the associated Security Group
- Select Edit inbound rules
- Important Notes
- Ensure HTTP (Port 80) is allowed
- Source should be set to 0.0.0.0/0 for public access
- Save the changes

- ❌ If HTTP is not allowed, the web server will not be accessible from the browser.
---

##⚡ Best Practices
- Always store your key pair securely
- Open only required ports in the security group
- User data scripts run only during the first boot
- To modify the user data script, a new instance launch is required

## 👨‍💻 Author

Kumlesh Kurre
IT Support & Network Engineer

⭐ If you find this project useful, please consider starring the repository.
