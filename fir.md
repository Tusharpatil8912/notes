Here's a README file that describes the process for setting up a VPC with public and private subnets, configuring internet access, and deploying instances on AWS.

---

# AWS VPC Setup with Public and Private Subnets

This guide covers the steps to set up a Virtual Private Cloud (VPC) with public and private subnets in AWS. The public subnet will have internet access, while the private subnet will connect to the internet via a NAT gateway.

## 1. Create a VPC

1. Go to the AWS Management Console.
2. Navigate to **VPC > Your VPCs > Create VPC**.
3. Configure the VPC:
   - **Name:** Tushar-patil
   - **CIDR Block:** 10.0.0.0/16
4. Click **Create VPC**.

## 2. Create a Public Subnet

1. Navigate to **Subnets > Create Subnet**.
2. Configure the public subnet:
   - **VPC:** Tushar-patil
   - **Subnet Name:** Tushar-public-subnet
   - **CIDR Block:** 10.0.0.0/25
3. Click **Create Subnet**.

## 3. Create a Private Subnet

1. Navigate to **Subnets > Create Subnet**.
2. Configure the private subnet:
   - **VPC:** Tushar-patil
   - **Subnet Name:** Tushar-private-subnet
   - **CIDR Block:** 10.0.0.128/25
3. Click **Create Subnet**.

## 4. Configure the Public Subnet

1. Select the **Tushar-public-subnet**.
2. Click **Actions > Edit subnet settings**.
3. Enable **Auto-assign IP settings** to allow resources to have public IPs.

## 5. Create and Attach an Internet Gateway

1. Navigate to **Internet Gateways > Create Internet Gateway**.
2. Name the gateway and click **Create**.
3. Select the created gateway, choose **Actions > Attach to VPC**, and select **Tushar-patil** VPC.

## 6. Configure the Route Table for the Public Subnet

1. Navigate to **Route Tables > Create Route Table**.
2. Name the table and associate it with **Tushar-patil** VPC.
3. Edit the route table:
   - Add a route for `0.0.0.0/0` and select the Internet Gateway (IGW).
4. Associate the route table with **Tushar-public-subnet**.

## 7. Launch EC2 Instances

### Public Instance

1. Go to **EC2 > Launch Instance**.
2. Select **Tushar-patil** VPC and **Tushar-public-subnet**.
3. Use the same key pair for SSH access.

### Private Instance

1. Go to **EC2 > Launch Instance**.
2. Select **Tushar-patil** VPC and **Tushar-private-subnet**.
3. Use the same key pair for SSH access.

## 8. Connect to the Public Instance and Test Internet Access

1. SSH into the public instance.
2. Test internet connectivity: 
   ```
   ping www.google.com
   ```

## 9. Connect to the Private Instance via Public Instance

1. SSH into the public instance.
2. Transfer the private key to the public instance.
3. Access the private instance using:
   ```
   ssh -i key.pem ubuntu@<Private-IP>
   ```
4. Verify connectivity within the private instance:
   ```
   ping www.google.com
   ```

## 10. Provide Internet Access to the Private Subnet

1. Create a NAT Gateway:
   - **Subnet:** Tushar-public-subnet
   - Allocate an Elastic IP
2. Attach the NAT Gateway to a route table:
   - Edit the private route table to add a route for `0.0.0.0/0` via the NAT Gateway.

