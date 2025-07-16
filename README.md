#  Deploying Nginx EC2 Server on AWS using Terraform (with Custom VPC, Subnets, IGW, Route Table)

## What this project does:

In this project, I created a simple EC2 server that installs and runs Nginx automatically using Terraform. I also created a custom VPC, subnets (public & private), internet gateway, route table, and security group. This project is done in the `eu-north-1` region with a specific free-tier eligible AMI.

## 🛠 What I did step-by-step:

### 1. **Initialized Terraform Provider**

### 2. **Created a Custom VPC**

I created a custom VPC with CIDR block `10.0.0.0/16`.

### 3. **Added Two Subnets**

One private (`10.0.1.0/24`) and one public (`10.0.2.0/24`). The public one has `map_public_ip_on_launch = true`.

### 4. **Attached Internet Gateway**

I attached an internet gateway to the VPC for external connectivity.

```hcl
resource "aws_internet_gateway" "my-igw" { ... }
```

### 5. **Created a Route Table and Association**

I added a route to `0.0.0.0/0` via the internet gateway, and associated it with the public subnet.


### 6. **Created Security Group for Nginx**

Allowed HTTP (port 80) from anywhere, and all outbound traffic.


### 7. **Launched EC2 Instance**

Used a free-tier compatible AMI (`ami-0c0e147c706360bd7`) and instance type `t3.nano`. Added a `user_data` script to install and start Nginx automatically.

### 8. **Output Values**

I used outputs to get the public IP and a clickable URL to access the Nginx page.


## Output:

After running `terraform apply`, I got:

* Nginx is installed and running automatically
* Public IP of the instance
* Direct URL to access Nginx server in browser

##  To Run this:

```bash
terraform init
terraform plan
terraform apply
```

Then copy the public IP or URL shown in the output and open it in your browser to see the Nginx welcome page.


