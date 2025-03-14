# Elastic Cloud Compute (EC2)
## Create an EC2 Instance
To create an EC2 instance in the **Mumbai** region (which is **ap-south-1**) using both the AWS Management Console and the AWS CLI, follow these steps.

<details>
   <summary>Creating an EC2 Instance in the Mumbai Region via AWS Management Console</summary>

### **1. Creating an EC2 Instance in the Mumbai Region via AWS Management Console:**

1. **Log into AWS Console**:
   Go to the [AWS Management Console](https://aws.amazon.com/console/), and log in with your credentials.

2. **Navigate to EC2 Console**:
   In the **search bar**, type **EC2** and click on **EC2** to open the EC2 dashboard.

3. **Change the Region**:
   - In the **top-right corner**, select the **Mumbai region** (ap-south-1) from the **region dropdown**.

4. **Launch Instance**:
   - Click on **Launch Instance** to begin the process of creating a new EC2 instance.

5. **Choose an AMI (Amazon Machine Image)**:
   - Select an AMI from the available options. For example, choose **Amazon Linux 2** or **Ubuntu**.

6. **Choose Instance Type**:
   - Choose an instance type like **t2.micro** (this is eligible for the **free tier**).
   - Click **Next: Configure Instance Details**.

7. **Configure Instance Details**:
   - Under **Network**, select your **VPC** or leave it as the default.
   - Under **Subnet**, choose any subnet in the Mumbai region (ap-south-1).

8. **Add Storage**:
   - You can adjust the storage size if necessary (default is usually fine).

9. **Configure Security Group**:
   - Create a new security group or select an existing one.
   - Ensure you add rules like **SSH (port 22)** for remote access if you're using Linux.

10. **Review and Launch**:
   - Review your configuration and click **Launch**.
   - If you don’t have an existing **Key Pair**, create one, download it, and then click **Launch Instances**.

11. **Access the Instance**:
   - After the instance is launched, you can view it in the EC2 dashboard.
   - Use the **Public IP** and **SSH Key** to access the instance via SSH:
     ```bash
     ssh -i "your-key.pem" ec2-user@your-public-ip
     ```
     
</details>


<details>
   <summary>Creating & Terminating an EC2 Instance in the Mumbai Region via AWS CLI</summary>
   
### **1. Creating an EC2 Instance in the Mumbai Region via AWS CLI:**

1. **Open Terminal**:
   Open your terminal or command prompt.

2. **Ensure AWS CLI is Configured**:
   Make sure your AWS CLI is configured with your credentials and default region. If not, run:
   ```bash
   aws configure
   ```

3. **Launch the EC2 Instance**:
   Use the `aws ec2 run-instances` command to launch an EC2 instance. Here’s the general syntax for creating an instance in the **Mumbai region** (`ap-south-1`).

   Example CLI command to launch an EC2 instance in Mumbai region:
   ```bash
   aws ec2 run-instances \
       --image-id ami-0abcdef1234567890 \  # Use a valid AMI ID for the Mumbai region
       --instance-type t2.micro \          # Instance type (e.g., t2.micro for free tier)
       --count 1 \                         # Number of instances to launch
       --region ap-south-1 \               # Mumbai region
       --key-name your-key-pair \          # Replace with your SSH key pair name
       --security-group-ids sg-xxxxxxxx \  # Replace with your security group ID
       --subnet-id subnet-xxxxxxxx        # Replace with your subnet ID
   ```

   - **image-id**: Use an appropriate AMI ID. For example, you can use the Amazon Linux 2 AMI ID in Mumbai.
     - Example AMI ID for Amazon Linux 2 in Mumbai region: `ami-0aef3c9d42a88f98f`
   - **key-name**: Replace with the name of the SSH key pair you want to use for accessing your instance.
   - **security-group-ids**: Use the ID of your security group that allows **SSH (port 22)** for Linux instances.
   - **subnet-id**: Use the ID of the subnet you want to launch the EC2 instance in. If you don’t know it, you can find it in the VPC dashboard.

<details>
   <summary>Click to view full command executed in the terminal:</summary>

   ```bash
   aws ec2 run-instances \
       --image-id ami-0f2ce9ce760bd7133 \
       --instance-type t2.micro \
       --count 1 \
       --region ap-south-1 \
       --key-name Myops \
       --security-group-ids sg-0106a2994ff8e49aa
       
   ```
   
</details>


4. **Verify the Instance**:
   After running the command, you can verify that the instance is launched by running:

   ```bash
   aws ec2 describe-instances --region ap-south-1
   ```

   This will show information about your running EC2 instances.

5. **Connect to Your EC2 Instance**:
   Once the instance is launched, you can connect to it via SSH. Use the **Public IP** or **Public DNS** of the instance:

   ```bash
   ssh -i "MyKeyPair.pem" ec2-user@your-public-ip
   ```

   Replace `MyKeyPair.pem` with your actual private key file and `your-public-ip` with the instance’s public IP address.


---
## 2. Terminate an Instance using AWS-CLI
- To terminate an EC2 instance using the AWS CLI, you can use the `terminate-instances` command. You need to specify the instance ID of the instance you want to terminate.
- Here's the general syntax:
```bash
aws ec2 terminate-instances --instance-ids i-xxxxxxxxxxxxxxxxx --region <your-region>
```
- Replace `i-xxxxxxxxxxxxxxxxx` with your actual instance ID and `<your-region>` with the region where the instance is running.

For example:
```bash
aws ec2 terminate-instances --instance-ids i-0967f588306e2c714 --region ap-south-1
```

You can find the instance ID by running:
```bash
aws ec2 describe-instances --region ap-south-1
```

This will return details about all your instances, including their instance IDs.

</details>

### **Summary:**

- **AWS Management Console**: Log in, navigate to EC2, and follow the steps to launch an instance in the Mumbai region.
- **AWS CLI**: Use the `aws ec2 run-instances` command with the appropriate AMI ID, instance type, key pair, security group, and subnet in the Mumbai region (`ap-south-1`).
