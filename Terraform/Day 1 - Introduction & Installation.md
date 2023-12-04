# Introduction to IaC
## Why Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is a systematic approach to managing and provisioning computing infrastructure through machine-readable script files, rather than through physical hardware configuration or interactive configuration tools. The adoption of IaC addresses several challenges associated with manual infrastructure configuration:

### Manual Configuration Challenges:

- **Time-Consuming:**
  - Manual configuration of infrastructure is a time-consuming process.

- **Error-Prone:**
  - Prone to errors and inconsistencies due to manual intervention.

- **Lack of Version Control:**
  - Lack of version control for configurations makes tracking changes difficult.

- **Heavy Reliance on Documentation:**
  - Heavy reliance on documentation for setup steps, which can quickly become outdated.

- **Limited Automation:**
  - Limited automation leads to slow provisioning of resources.

### Benefits of IaC:

- **Systematic, Automated, and Code-Driven Approach:**
  - IaC provides a systematic and code-driven approach to infrastructure management.

- **Enables Version Control:**
  - Infrastructure configurations can be version-controlled, enabling tracking of changes.

- **Reduces Manual Errors:**
  - Reduces manual errors and ensures consistency in infrastructure setups.

- **Facilitates Automation:**
  - Facilitates automation of provisioning and deployment processes.

- **Adaptable to Dynamic Requirements:**
  - Adaptable to dynamic application and service requirements.

## Different Infrastructure as Code Tools:

- **AWS: CloudFormation Template**
- **Azure: Resource Manager**
- **OpenStack: Heat Templates**

These tools provide a standardized way to define and manage infrastructure configurations, allowing for improved efficiency, reliability, and scalability.

# Why Terraform?

Terraform is a powerful Infrastructure as Code (IaC) tool that offers several compelling features, making it a preferred choice for DevOps and Cloud Engineers.

## Multi-Cloud Support:

- **Cloud-Agnostic Approach:**
  - Terraform follows a cloud-agnostic approach, allowing users to write infrastructure code that is not tied to any specific cloud provider.

- **Write Once, Deploy Anywhere:**
  - With Terraform, you can write your infrastructure code once and deploy it across various cloud providers, providing flexibility and reducing vendor lock-in.

## Large Ecosystem:

- **Extensive Collection of Providers and Modules:**
  - Terraform boasts a vast ecosystem with support for multiple cloud providers and a rich collection of modules. These modules offer pre-built configurations for a wide array of services.

- **Pre-Built Configurations:**
  - Leverage pre-built configurations to accelerate infrastructure provisioning and adhere to best practices.

## Declarative Syntax:

- **Specifies Desired End-State:**
  - Terraform uses a declarative syntax, enabling users to specify the desired end-state of their infrastructure. This makes configurations more readable and expressive.

## State Management:

- **Maintains a State File:**
  - Terraform maintains a state file that tracks the current state of your infrastructure. This enables informed decision-making during changes and updates.

## Plan and Apply Workflow:

- **Preview Changes:**
  - Use the `terraform plan` command to preview changes before applying them. This helps in understanding the impact of changes before they are executed.

- **Review and Approve Changes:**
  - Terraform's workflow involves reviewing and approving changes before applying them, ensuring a controlled deployment process.

## Community Support:

- **Active User Community:**
  - Benefit from an active user community for troubleshooting, sharing knowledge, and accessing valuable resources.

## Integration with Other Tools:

- **Versatile Integration:**
  - Terraform integrates seamlessly with various tools such as Docker, Kubernetes, Ansible, Jenkins, etc. This allows for the creation of comprehensive automation pipelines.

## HCL Language:

- **HashiCorp Configuration Language (HCL):**
  - Terraform uses HCL, a language specifically designed for defining infrastructure. HCL is human-readable and expressive, making it easy for both developers and operators.

## Competitors of Terraform:

- **Crossplane**
- **Pulumi**

Explore Terraform's unique features and capabilities to efficiently manage and automate your infrastructure.

---
# Installation of Terraform

## Windows Installation

### Download Terraform

1. Visit the official Terraform website: [https://www.terraform.io/downloads.html](https://www.terraform.io/downloads.html)
2. Select the **Windows** operating system.
3. Under Binary Downloaded for Windows, choose the appropriate version (e.g., 386 Version 1.5.x).

### Extract the Terraform Executable

4. After downloading the ZIP file, extract its contents to a directory of your choice.

### Add Terraform to Your System PATH

5. Right-click on the Windows Start button and select "System."
6. Click on "Advanced system settings" on the left.
7. In the "System Properties" window, click the "Environment Variables" button.
8. In the "System Variables" section, find and select the "Path" variable, then click "Edit."
9. Click "New" and add the path to the directory containing the Terraform executable (e.g., C:\Path\To\Terraform).
10. Click "OK" to save the changes.

### Verify the Installation

11. To verify that Terraform is correctly installed, open a new Command Prompt or PowerShell window and run the following command:

    ```bash
    terraform -version
    ```

    This command should display the installed Terraform version, confirming that it's working correctly.

### Install Terraform Extension for VSCode

12. In VSCode, go to the Extensions view by clicking the square icon on the left sidebar or using the shortcut `Ctrl+Shift+X` (Windows).
13. In the Extensions view, search for "Terraform."
14. Find the "HashiCorpTerraform" extension published by Microsoft, and click the "Install" button.

# Install Terraform on Linux

## Ubuntu/Debian

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

## CentOS/RHEL

```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install terraform
```

## Amazon Linux

```
sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
```
### Verify the Installation
To verify that Terraform is correctly installed, open a new terminal and run the following command:
```
terraform -version
```
This command should display the installed Terraform version, confirming that it's working correctly.

# Install Terraform on macOS

## Using Homebrew

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```
### Verify the Installation
To verify that Terraform is correctly installed, open a new terminal and run the following command:
```
terraform -version
```
This command should display the installed Terraform version, confirming that it's working correctly.


# GitHub Codespaces Usage Guide

## What is GitHub Codespace?

GitHub Codespace is a cloud-based, containerized development environment provided by GitHub. It offers a sandbox environment with 2 CPUs and 4 GB of RAM, free for 60 hours per month.

## Using GitHub Codespaces

### Prerequisites

1. **GitHub Account:**
   - Login to your GitHub account.

2. **Repository:**
   - Create a new repository or choose an existing one.

### Creating a Codespace

1. Click on the "Code" button in your repository.

2. Select "Codespaces" from the dropdown menu.

3. Click "Create Codespace in Main."

4. Codespaces will provide you a virtual machine with Ubuntu and VS Code by default.

5. Follow the steps provided in the Downloads Page for Linux.

### Customizing Codespace Environment

#### Step 1 - Add Terraform Configuration

- Navigate to the `dev` section.
- Select "Codespaces: Add Dev Container Configuration Files."
- Click "Modify your active configuration."
- Search for "terraform."
- Select "terraform, tflint, and TFGrunt devcontainers."
- Click "OK."
- Keep defaults.

#### Step 2 - Add AWS Configuration

- Navigate to the `dev` section.
- Select "Codespaces: Add Dev Container Configuration Files."
- Click "Modify your active configuration."
- Search for "AWS."
- Select "AWS CLI environments."
- Click "OK."
- Keep defaults.

#### Step 3 - Rebuild Container

- Navigate to the `rebuild` section.
- Click "Codespace: Rebuild Container."
- Click "Rebuild."
- This step creates a new container environment with AWS CLI and Terraform installed.

### Verify Installation

- Run the following commands:
  ```bash
  terraform --version
  ```
  ```
  aws version --version
  ```

### Important Note
Do not delete the .devcontainer file.


## Configure AWS in VSCode

**Note: It is highly recommended to use an IAM user. DevOps/Cloud engineers should not have Root Access.**

1. Open VSCode and select your user name.

2. Click on "Security Credentials."

3. Under Access Keys, click "Create Access Key."

4. It will generate an Access Key ID and Secret Access Key. Download the CSV file containing these credentials.


To use Terraform with AWS, you need to configure AWS credentials. Follow the steps below to set up your AWS credentials in VSCode or Codespaces.
#### Open Terminal in VSCode or Codespaces & Run AWS Configuration Command


```
aws configure
```
Execute the following command to configure your AWS credentials:

```
AWS Access Key Id - AKIAS47ML2SGH2HEK7V3  #  Give like the one which is generated for You # I intentionally given wrong
AWS Secret Access Key - Z1m6Q3G9Q7LbJSyzepde3K715EOFK5Ka+fIvw6L8 # Give your secret access key # I intentionally given wrong
Default Region - us-east-1 # Give your specified region 
Default output format - json # Give your specified format
```



# Configuring AWS for Terraform

## Step 1: Setup Provider Configuration

In VSCode, create a file named `main.tf` for the main configuration of the Terraform script.

```hcl
# main.tf

provider "aws" {
  region = "us-east-1"  # Replace with your desired region
}
```

## Step 2: Define AWS Resource
Define the AWS resource block for an EC2 instance in the same main.tf file.

```
# main.tf

provider "aws" {
  region = "us-east-1"  # Replace with your desired region
}

resource "aws_instance" "myfirstinstance" {
  ami           = "ami-0230bd60aa48260c6"  # Replace with the appropriate AMI ID
  instance_type = "t2.micro"
}
```

## Step 3: Run Terraform Commands
### Step 3.1: Initialize Terraform
```
terraform init
```
This command initializes the configuration and fetches necessary details from AWS. It creates .terraform and .terraform.lock.hcl.

### Step 3.2: Preview Changes
```
terraform plan
```
This command performs a dry run, showing what resources will be created or modified.

### Step 3.3: Apply Changes
```
terraform apply
```
This command applies the changes and creates the AWS EC2 instance.

### Handling Errors
If errors occur (e.g., InvalidAMID or MissingInput), review the error messages, and modify the configuration accordingly.

## Additional Configuration: Adding Key and Tags
To add key and tags to the EC2 instance, modify the main.tf file.
```
# main.tf

provider "aws" {
  region = "us-east-1"  # Replace with your desired region
}

resource "aws_instance" "myec2" {
  ami           = "ami-0230bd60aa48260c6"  # Replace with the appropriate AMI ID
  instance_type = "t2.micro"
  key_name      = "mykey"
  tags = {
    Name = "terraformcreatedec2"
  }
}
```
#### Applying Changes with Key and Tags
```
terraform apply
```
#### Destroy previous instance and create new instance
```
terraform destroy
```

# Terraform Lifecycle and State File Basics

## Terraform Lifecycle

Terraform follows a lifecycle process for managing infrastructure. Here are the key commands in the Terraform lifecycle:

- **terraform init:** Initialize the configuration. This command sets up the working directory, downloads necessary plugins, and initializes the backend.

- **terraform plan:** Preview changes. This command generates an execution plan that describes what Terraform will do to reach the desired state.

- **terraform apply:** Apply changes. This command executes the changes proposed in the execution plan. It creates, modifies, or deletes resources to match the desired state.

- **terraform destroy:** Destroy resources. This command is used to destroy the Terraform-managed infrastructure. It deletes all the resources created during the apply phase.

## Basics of Terraform State File

Terraform uses a state file to track the current state of the infrastructure. The state file is crucial for future changes and resource management. Here are the basics of the Terraform state file:

- **File Name:** The default name for the state file is `terraform.tfstate`.

- **Tracking State:** The state file tracks the current state of resources created by Terraform.

- **Necessary for Changes:** The state file is necessary for making future changes to the infrastructure. Terraform uses it to understand the current state and what changes are needed.

- **Security:** The state file contains sensitive information, and it should be kept secure. Never share it or store it in an insecure location.


