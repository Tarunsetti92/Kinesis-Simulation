# AWS Kinesis, EC2, and Apache Flink Studio Setup Guide

## 1. Create AWS Kinesis Data Stream

1. **Login to AWS Console**
2. Navigate to **Kinesis** service.
3. Select **Data Streams** > **Create data stream**.
4. Enter a stream name (e.g., `my-stream`), set the number of shards, and create it.

---

## 2. Launch an EC2 Instance

1. Go to **EC2** service in AWS Console.
2. Click **Launch Instance**.
   - Choose an AMI (e.g., Amazon Linux 2023 or Ubuntu).
   - Select an instance type (e.g., t2.micro for testing).
   - Configure a key pair for SSH (create one if you don’t have).
   - Configure the security group to allow SSH (port 22).
3. Click **Launch**.

---

## 3. Connect to the EC2 Instance

1. Get the **public DNS** or **IP** from the EC2 dashboard.
2. Connect from your terminal:
   ```bash
   ssh -i /path/to/your-key.pem ec2-user@<ec2-public-dns>
   ```
   - Use `ubuntu` instead of `ec2-user` for Ubuntu AMI.

---

## 4. Create `script.py` Using Vim

1. On the EC2 instance:
   sudo su -  (root permission)
   vim script.py
3. Press `i` for insert mode, paste your Python code.
4. Press `Esc`, then type `:wq` and press `Enter` to save and exit.

## 5. Install Python and Boto3 and aws configure 

```bash
yum install python3 -y   # Amazon Linux
# or
apt-get install python3 -y   # Ubuntu

yum install python3-pip -y

pip install boto3
```
** Run the configuration:**
   ```bash
   aws configure
**Enter your IAM credentials: Got to IAM > Security credentials > Create access key**
   - Access Key ID
   - Secret Access Key
   - Default region (e.g., us-east-1)
   - Output format (e.g., json)

<img width="377" height="62" alt="image" src="https://github.com/user-attachments/assets/4676ff09-9808-4496-ae2e-b823f8ff15c7" />

python3 script.py

**6. Create Apache Flink – Studio Notebook**

1. In AWS Console, go to **Kinesis Data Analytics**.
2. Click **Studio notebooks**.
3. Click **Create Studio notebook**.
4. Choose a method to setup the Studio notebook ( Quick create with sample code ) > Provide a name > AWS Glue database > create a database and connect it and click on Create Studio notebook
5. Open the notebook and click on run
6. Once the notebook is preoared > click on **Open in Apache Zeppelin**
7. Create a new note in Zeppelin and provide a name
8. copy the test.sql code and run the note , if any error comes outfor permissions . Go to IAM > OPEN the role > add permission > **AWSGlueConsoleFullAccess** and save the changes
9.Run the code again and code will pass
10. Run the select statement to get the data 



## Summary Checklist

- [x] Kinesis stream created
- [x] EC2 launched and connected via SSH
- [x] `script.py` created with code via Vim
- [x] AWS CLI configured with IAM credentials
- [x] (Optional) Python and boto3 installed
- [x] Apache Flink Studio notebook created

---
