# Teardown Guide  
AWS VPC & Security Group Lab

This document describes how to safely delete all AWS resources created in this lab to avoid unnecessary charges.

---

## ⚠️ Important Notes

- Ensure you no longer need the resources before deleting them.
- Deleting resources is **irreversible**.
- Always verify that the AWS region is correct.

---

## 🧹 Resources to Delete (Recommended Order)

### 1️⃣ Terminate EC2 Instances
Delete all EC2 instances created in this project.

- APP EC2
- DB EC2

**Steps:**
1. Go to **EC2 → Instances**
2. Select the instances
3. Click **Instance state → Terminate instance**

✅ This will stop compute charges.

---

### 2️⃣ Delete Elastic IPs (If Any)
If you allocated an Elastic IP, make sure to release it.

**Steps:**
1. Go to **EC2 → Elastic IPs**
2. Select the Elastic IP
3. Click **Release Elastic IP address**

⚠️ Elastic IPs incur charges when not attached.

---

### 3️⃣ Delete EBS Volumes
Check for leftover EBS volumes after terminating EC2.

**Steps:**
1. Go to **EC2 → Volumes**
2. Delete any volumes in `available` state

📌 Free Tier includes limited EBS usage. Extra volumes may incur costs.

---

### 4️⃣ Delete Security Groups
Delete custom security groups created for this lab.

- `sg-app`
- `sg-db`

**Steps:**
1. Go to **VPC → Security Groups**
2. Ensure they are not attached to any resources
3. Delete the security groups

---

### 5️⃣ Delete Route Tables
Delete custom route tables:

- `public-rt`
- `private-rt`

**Steps:**
1. Go to **VPC → Route Tables**
2. Remove subnet associations
3. Delete the route tables

---

### 6️⃣ Delete Subnets
Delete all subnets created in the VPC.

- Public subnet
- Private subnet

**Steps:**
1. Go to **VPC → Subnets**
2. Select subnets
3. Delete

---

### 7️⃣ Detach and Delete Internet Gateway
**Steps:**
1. Go to **VPC → Internet Gateways**
2. Detach the IGW from the VPC
3. Delete the Internet Gateway

---

### 8️⃣ Delete the VPC
Finally, delete the VPC.

**Steps:**
1. Go to **VPC → Your VPCs**
2. Select `MyVPC`
3. Delete VPC

---

## ✅ Final Verification

After teardown, verify that no resources remain:

- EC2 instances
- EBS volumes
- Elastic IPs
- VPCs
- Security groups

You can confirm this by checking the **AWS Billing Dashboard**.

---

## 💡 Best Practice

- Always tear down lab environments after testing.
- Use Infrastructure as Code (Terraform / CloudFormation) for easier cleanup.
- Monitor costs regularly using AWS Cost Explorer.

---

## 🏁 Conclusion

This teardown ensures:
- Zero unnecessary AWS charges
- Clean AWS account
- Safe Free Tier usage

End of teardown process.
