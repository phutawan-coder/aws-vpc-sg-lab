# VPC with Public App and Private DB Setup Guide

This document describes the step-by-step setup of an AWS VPC environment using a **public application tier** and a **private database tier**, following basic cloud and security best practices.

---

## Architecture Overview

- **VPC CIDR**: `10.0.0.0/16`
- **Public Subnet**: For Application EC2
- **Private Subnet**: For Database EC2
- **Security Groups**: Isolated access between App and DB
- **Internet Access**: Public subnet only

---

## Step-by-Step Setup

### 1. Create a VPC
- Create a VPC named **`MyVPC`**
- Set CIDR block to: `10.0.0.0/16`

---

### 2. Create a Public Subnet
- Use **MyVPC**
- Enable:
- ✅ Auto-assign public IPv4 address
- This subnet will host the **Application EC2**

---

### 3. Create a Private Subnet
- Use **MyVPC**
- Do **NOT** enable:
- ❌ Auto-assign public IPv4 address
- This subnet will host the **Database EC2**

---

### 4. Create Route Tables
Create two route tables using **MyVPC**:

- **public-rt**
- **private-rt**

---

### 5. Associate Subnets with Route Tables
- Associate:
- Public Subnet → `public-rt`
- Private Subnet → `private-rt`

---

### 6. Create an Internet Gateway
- Create an **Internet Gateway**
- Attach it to **MyVPC**

---

### 7. Configure Public Route Table
- Add a route to `public-rt`:

---

### 8. Create Security Groups
Create two security groups under **MyVPC**:

- **sg-app**
- **sg-db**

---

### 9. Configure `sg-app` Inbound Rules
Allow SSH access **only from your own IP**:

- Type: SSH
- Port: 22
- Source: My IP

---

### 10. Configure `sg-db` Inbound Rules
Allow SSH access **only from the App EC2**:

- Type: SSH
- Port: 22
- Source: `sg-app`

> This ensures the database is not directly accessible from the internet.

---

### 11. Launch EC2 Instances
Create two EC2 instances:

#### Application EC2
- Subnet: Public Subnet
- Security Group: `sg-app`
- Public IP: Enabled

#### Database EC2
- Subnet: Private Subnet
- Security Group: `sg-db`
- Public IP: Disabled

---

## Expected Result

- ✅ SSH access to **App EC2** is allowed only from your local machine
- ✅ SSH access to **DB EC2** is allowed only from **App EC2**
- ❌ Direct SSH access to DB from the internet is blocked

---

## Notes
- This setup demonstrates **network isolation**, **least privilege access**, and **basic cloud security design**
- Resources can be safely terminated after testing to avoid unnecessary costs

---

