# Automating Flask Application Testing Infrastructure with Terraform Provisioners

## Scope
The Terraform project aims to automate the infrastructure setup for the XYZ Development Team's Flask application (app.py). The primary goal is to facilitate efficient testing of changes made to the application by creating a dedicated environment. The scope includes the creation of a VPC, a public subnet, a Route Table with an Internet Gateway, and the deployment of the Flask application on an EC2 instance. The environment should be externally accessible, allowing developers to verify their application's functionality using a provided URL.

## Benefits
Manually performing these tasks for each developer would take approximately one hour, but automating this with Terraform significantly reduces the setup time. This is crucial for saving time across multiple developers and projects within the XYZ Development Team.

## Scenario

A developer has shared the app.py file, a Flask application, and would like to verify its functionality. The application provides a simple "Hello, Terraform!" message when accessed.

```
# app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello, Terraform!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=80)
```
## Approach
### Objective:
This Terraform configuration automates the setup of AWS infrastructure and deploys a Flask application (app.py) on an EC2 instance. The infrastructure includes a VPC, a public subnet, an Internet Gateway, a Route Table, a security group, and an EC2 instance.

```
# Provider Configuration: This block defines the AWS provider configuration, specifying the region where the AWS resources will be created.

provider "aws" {
  region = "us-east-1"  # Replace with your desired AWS region.
}

# Variable Definition: Declares a variable named cidr with a default value of "10.0.0.0/16". This variable will be used for the VPC CIDR block.

variable "cidr" {
  default = "10.0.0.0/16"
}

# The command ssh-keygen -t rsa is used to generate a new SSH key pair on your local workstation. 
# Key Pair Resource: Creates an AWS key pair resource, which is used for SSH access to EC2 instances. It specifies the key name and the public key file.

resource "aws_key_pair" "example" {
  key_name   = "terraform-pavan" 
  public_key = file("~/.ssh/id_rsa.pub")
}

# VPC Resource: Defines an AWS Virtual Private Cloud (VPC) resource using the CIDR block specified in the cidr variable.

resource "aws_vpc" "myvpc" {
  cidr_block = var.cidr
}

# Subnet Resource: Creates a subnet in the specified availability zone within the VPC, enabling public IP assignment to instances launched in this subnet.

resource "aws_subnet" "sub1" {
  vpc_id                  = aws_vpc.myvpc.id
  cidr_block              = "10.0.0.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true
}

# Internet Gateway Resource: Creates an internet gateway and associates it with the VPC.

resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.myvpc.id
}


# Route Table Resource: Defines a route table with a default route pointing to the internet gateway.

resource "aws_route_table" "RT" {
  vpc_id = aws_vpc.myvpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }
}

# Route Table Association Resource: Associates the route table with the subnet.

resource "aws_route_table_association" "rta1" {
  subnet_id      = aws_subnet.sub1.id
  route_table_id = aws_route_table.RT.id
}


# Security Group Resource: Creates a security group allowing inbound traffic on ports 80 (HTTP) and 22 (SSH).

resource "aws_security_group" "webSg" {
  name   = "web"
  vpc_id = aws_vpc.myvpc.id

  ingress {
    description = "HTTP from VPC"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "Web-sg"
  }
}

# EC2 Instance Resource: Launches an EC2 instance with specified AMI, instance type, key pair, security group, and subnet.

resource "aws_instance" "server" {
  ami                    = "ami-0261755bbcb8c4a84"
  instance_type          = "t2.micro"
  key_name      = aws_key_pair.example.key_name
  vpc_security_group_ids = [aws_security_group.webSg.id]
  subnet_id              = aws_subnet.sub1.id

# Connection and Provisioners for EC2 Instance: Defines the SSH connection details for provisioning.

connection {
  type        = "ssh"
  user        = "ubuntu"
  private_key = file("~/.ssh/id_rsa")
  host        = self.public_ip
}

# Copies the local app.py file to the remote instance.
# File Provisioner: The file provisioner is responsible for copying files from the local machine to the remote machine. In your case, it copies the app.py file from your local machine to the EC2 instance.

provisioner "file" {
  source      = "app.py"
  destination = "/home/ubuntu/app.py"
}

# Remote-Exec Provisioner: The remote-exec provisioner is used to execute commands on the remote machine. In your configuration, it performs various tasks on the EC2 instance, such as updating packages, installing Python packages, and running the app.py application.

provisioner "remote-exec" {
  inline = [
    "echo 'Hello from the remote instance'",
    "sudo apt update -y",
    "sudo apt-get install -y python3-pip",
    "cd /home/ubuntu",
    "sudo pip3 install flask",
    "sudo python3 app.py &",
  ]
}

# These provisions assume you have an app.py file in the same directory as your Terraform configuration file. The inline script installs necessary packages and starts the Flask application.

```
### Run the following Terraform commands:
```
terraform init
```
```
terraform apply
```

#### Here's a step-by-step guide to checking the login into a particular EC2 instance and ensuring everything is working fine using Terraform:

### SSH into the EC2 Instance:
Open a new terminal tab and run the following command to SSH into the EC2 instance:
```
ssh -i ~/.ssh/id_rsa ubuntu@<ec2-instance>
```
Type "yes" when prompted to confirm the connection.

### Check the Deployed Application:
Once logged into the EC2 instance, run the following command to list files in the home directory:
```
ls
```
You should see the app.py file in the /home/ubuntu directory.

###  Access the Application:

Open a web browser and navigate to the public IP address of your EC2 instance
```
http://<public-ip>
```
This should display your deployed application which is Hello, Terraform!

This project demonstrates an automated approach to deploying infrastructure and applications using Terraform, making use of provisioners for zero-touch automation.

### Overview

1. **Infrastructure as Code (IaC):**
   - The project utilizes Terraform for defining and provisioning infrastructure as code, allowing for easy management and versioning of infrastructure configurations.

2. **Provisioners for Automation:**
   - Terraform provisioners automate the configuration and deployment of software on the provisioned infrastructure. This eliminates the need for manual intervention.

3. **Zero Touch Automation:**
   - The concept of "Zero Touch Automation" is realized by executing `terraform apply`, which automates the entire process, including infrastructure creation and application deployment.

4. **Developer Productivity:**
   - Developers can focus on writing code and defining infrastructure configurations. The deployment process is standardized and automated, leading to increased productivity.

5. **CI/CD Integration:**
   - When integrated with CI/CD pipelines, developers can trigger deployments seamlessly. Changes can be deployed automatically upon pushing to version control or through CI/CD tools.

6. **DevOps Role:**
   - DevOps engineers play a crucial role in designing and maintaining infrastructure-as-code templates, setting up CI/CD pipelines, and ensuring a smooth end-to-end automation process.

7. **Zero Touch Testing:**
   - Developers can efficiently test applications by accessing provisioned resources without manual intervention, enabling rapid testing of changes.


# Provisioners 
Let's explore the functionalities of the file, remote-exec, and local-exec provisioners in Terraform through detailed examples for each.

## file Provisioner:
The file provisioner is used to copy files or directories from the local machine to a remote machine. This is useful for deploying configuration files, scripts, or other assets to a provisioned instance.

```
resource "aws_instance" "example" {
  ami           = "ami-0261755bbcb8c4a84"
  instance_type = "t2.micro"
}

provisioner "file" {
  source      = "local/path/to/localfile.txt"
  destination = "/path/on/remote/instance/file.txt"
  connection {
    type        = "ssh"
    user        = "ec2-user"
    private_key = file("~/.ssh/id_rsa")
    host        = aws_instance.example.public_ip
  }
}
```
In this example, the file provisioner copies the localfile.txt from the local machine to the /path/on/remote/instance/file.txt location on the AWS EC2 instance using an SSH connection.

## remote-exec Provisioner:

The remote-exec provisioner is used to run scripts or commands on a remote machine over SSH or WinRM connections. It's often used to configure or install software on provisioned instances.

```
resource "aws_instance" "example" {
  ami           = "ami-0261755bbcb8c4a84"
  instance_type = "t2.micro"
}

provisioner "remote-exec" {
  inline = [
    "sudo yum update -y",
    "sudo yum install -y httpd",
    "sudo systemctl start httpd",
  ]

  connection {
    type        = "ssh"
    user        = "ec2-user"
    private_key = file("~/.ssh/id_rsa")
    host        = aws_instance.example.public_ip
  }
}
```
In this example, the remote-exec provisioner connects to the AWS EC2 instance using SSH and runs a series of commands to update the package repositories, install Apache HTTP Server, and start the HTTP server.

## local-exec Provisioner:
The local-exec provisioner is used to run scripts or commands locally on the machine where Terraform is executed. It is useful for tasks that don't require remote execution, such as initializing a local database or configuring local resources.

```
resource "null_resource" "example" {
  triggers = {
    always_run = "${timestamp()}"
  }

  provisioner "local-exec" {
    command = "echo 'This is a local command'"
  }
}
```
In this example, a null_resource is used with a local-exec provisioner to run a simple local command that echoes a message to the console whenever Terraform is applied or refreshed. The timestamp() function ensures it runs each time.






