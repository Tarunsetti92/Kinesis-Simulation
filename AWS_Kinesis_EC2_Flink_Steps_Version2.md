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
   ```bash
   vim script.py
   ```
2. Press `i` for insert mode, paste your Python code.
3. Press `Esc`, then type `:wq` and press `Enter` to save and exit.

---

## 5. Configure AWS CLI Using IAM User

1. **Install AWS CLI** (if not pre-installed):
   - Amazon Linux:
     ```bash
     sudo yum install awscli -y
     ```
   - Ubuntu:
     ```bash
     sudo apt-get install awscli -y
     ```
2. Run the configuration:
   ```bash
   aws configure
   ```
3. Enter your IAM credentials:
   - Access Key ID
   - Secret Access Key
   - Default region (e.g., us-east-1)
   - Output format (e.g., json)

---

## 6. (Optional) Install Python and Boto3

```bash
sudo yum install python3 -y   # Amazon Linux
# or
sudo apt-get install python3 -y   # Ubuntu

pip3 install boto3
```

---

## 7. Create Apache Flink – Studio Notebook

1. In AWS Console, go to **Kinesis Data Analytics**.
2. Click **Studio notebooks**.
3. Click **Create Studio notebook**.
4. Provide a name, select your Kinesis stream as a source, and create.
5. Open the notebook and start writing Flink code (Scala, Python, or SQL).

---

## Example: Minimal Python Script to Write to Kinesis

```python
import boto3

kinesis = boto3.client('kinesis', region_name='us-east-1')

data = 'Hello Kinesis!'
response = kinesis.put_record(
    StreamName='my-stream',
    Data=data.encode('utf-8'),
    PartitionKey='partition-1'
)
print(response)
```

---

## Summary Checklist

- [x] Kinesis stream created
- [x] EC2 launched and connected via SSH
- [x] `script.py` created with code via Vim
- [x] AWS CLI configured with IAM credentials
- [x] (Optional) Python and boto3 installed
- [x] Apache Flink Studio notebook created

---