# aws-vpc-3tier-deployment

# 🌐 AWS 3-Tier Web Application Deployment (LEMP Stack)

A fully functional **3-Tier Web Registration Application** deployed on **Amazon Web Services (AWS)** using a **LEMP Stack** (Linux, Nginx, MySQL, PHP).

This project demonstrates how to **design, configure, and deploy** a secure and scalable student registration system following **industry-standard AWS best practices**.

---

## 🏗️ Architecture Overview

The application follows a **classic 3-tier model**:

| Tier | Component | Function | Network Placement |
|------|------------|-----------|------------------|
| **Web Tier** | Nginx + HTML | Handles frontend requests | Public Subnet |
| **Application Tier** | PHP | Processes business logic | Private Subnet |
| **Database Tier** | MySQL | Stores data securely | Private Subnet |

**Flow:**  
`User → Web Server → App Server → Database Server`

---

## ⚙️ Tech Stack

- **Cloud Platform:** AWS (VPC, Subnets, Route Tables, NAT Gateway, Internet Gateway, Elastic IPs, EC2 Instances)
- **Frontend:** HTML, CSS  
- **Backend:** PHP  
- **Database:** MySQL  
- **Web Server:** Nginx  
- **OS:** Amazon Linux 2  

---

## ☁️ AWS Infrastructure Setup

### 1️⃣ VPC and Subnets
- Custom VPC: `10.0.0.0/16`  
- Subnets:
  - `web-subnet` → Public  
  - `app-subnet` → Private  
  - `db-subnet` → Private  
- Each subnet placed in a **different Availability Zone**

### 2️⃣ Route Tables
- **Public Route Table** → connected to Internet Gateway  
- **Private Route Table** → connected to NAT Gateway  

### 3️⃣ EC2 Instances
| Server | Placement | Purpose |
|---------|------------|----------|
| **Web Server** | Public | Serves frontend (HTML/Nginx) and routes traffic to App Server |
| **App Server** | Private | Runs PHP backend logic |
| **DB Server** | Private | Hosts MySQL database |

---

## 🔒 Security Group Configuration

| Server | Allowed Source | Allowed Ports | Purpose |
|---------|----------------|---------------|----------|
| **Web Server** | 0.0.0.0/0 | 80 (HTTP) | Public access |
| **App Server** | Web SG | 80 (HTTP) | Accepts traffic from Web Tier |
| **DB Server** | App SG | 3306 (MySQL) | Accepts traffic from App Tier |

---

## 🚀 Deployment Steps

### 🧩 Web Server
```bash
sudo yum install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
