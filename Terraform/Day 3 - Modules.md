# Monolithic Architecture Challenges and Terraform Modules in IaC Projects

## Real-Life Example:

Imagine you're working in an organization called example.com. This organization utilizes a monolithic architecture for its software development. The codebase, comprising millions of lines of Java source code, forms a single application or project. In this monolith, all one million lines of code are tightly integrated into a singular structure.

## Monolithic Architecture Challenges:

### 1. Bug Identification and Understanding:
- **Issue:** Bugs are hard to locate and understand in a massive codebase.
- **Consequence:** New team members may struggle, leading to significant time delays.

### 2. Lack of Ownership:
- **Issue:** No clear ownership of specific code sections.
- **Consequence:** Assigning and tracking bugs becomes challenging, hindering accountability.

### 3. Maintenance Difficulty:
- **Issue:** Maintaining and upgrading is complex.
- **Consequence:** Regular maintenance, updates, and addressing security vulnerabilities become cumbersome.

### 4. Testing Challenges:
- **Issue:** Testing the entire application is time-consuming.
- **Consequence:** Development cycle inefficiency.

## Transition to Microservices:

- **Solution:** Move from monolithic to microservices architecture.
- **Benefits:**
  - **Bug Isolation:** Services are smaller, making bug identification more manageable.
  - **Ownership:** Each microservice is owned, ensuring clear responsibility.
  - **Maintenance:** Easier to maintain and upgrade individual services independently.
  - **Testing:** Testing can be focused on specific microservices, facilitating quicker testing.

## Applying the Concept to Terraform:

### 1. Terraform Monolith:
- **Scenario:** One Terraform project for all resources needed by a development team.
- **Issue:** Similar challenges as in monolithic software applications.

### 2. Module Approach:
- **Solution:** Adopt a modular approach in Terraform.
- **Benefits:**
  - **Ownership:** Each module can be owned and maintained by a specific DevOps team.
  - **Reuse:** Modules can be reused across different development teams.
  - **Isolation:** Changes and bug fixes can be isolated to specific modules, easing testing and deployment.

### 3. Pull Request Challenges:
- **Challenge:** Pull requests may involve changes across different modules.
- **Solution:** Implement careful versioning and testing strategies to prevent unintentional impacts.

## Conclusion:

- **Summary:** Transitioning from monolithic to modular approaches enhances clarity, ownership, maintenance, and testing efficiency.
- **Takeaway:** Microservices and modularization principles are crucial for scalability, maintainability, and collaborative development in large and complex systems.

## Terraform Modules in IaC Projects:

### Modularity:

- Break down infrastructure into smaller, self-contained components.
- Each module handles a specific function, making it easier to manage and understand.

### Reusability:

- Create reusable templates for common infrastructure components.
- Reduce duplication by using modules across different Terraform projects, ensuring consistency.

### Simplified Collaboration:

- Facilitate collaboration by enabling teams to work on separate modules independently.
- Combine modules to build complex infrastructure, streamlining development and reducing conflicts.

### Versioning and Maintenance:

- Modules have their own versioning for easier update and change management.
- Projects using a module can choose when to adopt a new version, preventing unexpected changes.

### Abstraction:

- Abstract away complexity of underlying resources within a module.
- Focus on high-level parameters, making it easier to configure and manage.

### Testing and Validation:

- Modules can be individually tested and validated, reducing the risk of errors.

### Documentation:

- Modules promote self-documentation.
- Clearly define variables, outputs, and resource dependencies within a module for easy understanding and usage.

### Scalability:

- Provide a scalable approach as your infrastructure grows.
- Create new modules for different components, maintaining a clean and organized codebase.

### Security and Compliance:

- Encapsulate security and compliance best practices within modules.
- Ensure consistency and compliance across deployments.


# Terraform AWS EC2 Configuration

## Objective

The objective of this Terraform project is to create an AWS EC2 instance using Terraform, emphasizing the use of variables for flexibility and a `terraform.tfvars` file for managing configuration values. Additionally, an `output.tf` file is included to display relevant information after applying the Terraform configuration.

#### Create main.tf file:

- Purpose: Define the AWS provider and an EC2 instance.
```
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = var.ami_value
  instance_type = var.instance_type_value
}
```
#### Create variables.tf file:

- Purpose: Declare variables to make the configuration flexible.
```
variable "ami_value" {
  description = "value for the ami"
}

variable "instance_type_value" {
  description = "value for the instance_type"
}
```

#### Create terraform.tfvars file:

- Purpose: Store specific variable values without exposing sensitive information in source code.
```
ami_value            = "ami-0fc5d935ebf8bc3bc"
instance_type_value  = "t2.micro"
```

#### Create output.tf file:
- Purpose: Display relevant information after applying the Terraform configuration.
```
output "public_ip" {
  value = aws_instance.example.public_ip
}
```
#### Initialize Terraform:
- Purpose: Initialize the working directory and download any required providers.
```
terraform init
```
#### Plan the Terraform configuration:
- Purpose: Preview changes before applying the configuration, ensuring correctness.
```
terraform plan
```

#### Apply the Terraform configuration:
- Purpose: Apply the planned changes to create AWS resources.
```
terraform apply
```

#### Review the Output:
- Purpose - Verify that the EC2 instance has been created and view the public IP address as specified in the output.tf file. I got output like below
```
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

public_ip = "3.80.195.161"
```

##### Notes:

- Developers can customize variable values in the terraform.tfvars file without modifying the main Terraform configuration.
- Sensitive information, such as API keys or passwords, should be excluded from version control by adding the corresponding files to the .gitignore file.
- Ensure proper documentation or communication with the team regarding the creation and usage of the terraform.tfvars file.


# Modularizing a Terraform project involves systematically organizing and restructuring the code 

### Certainly! Let's break down the steps to modularize your Terraform project:

#### Step 1: Create Module Folder
Create a new folder named ```modules/ec2_instance``` in the same directory where you have your Terraform code.

#### Step 2: Move Files to Module Folder
Move the main.tf, variables.tf, and outputs.tf files from your main project directory to the modules/ec2_instance folder.

#### Step 3: Delete terraform.tfvars
Since you are creating a module, you don't need the terraform.tfvars file. Delete it.

#### Step 4: Create a main.tf file outside the modules/ec2_instance folder
Create a new main.tf file in the root folder for any user of the module. In this file, you'll define the provider and reference the module.

##### Organize the folder structure accordingly like below
```
/your_project
├── main.tf
└── /modules
    └── /ec2_instance
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

#### Step 5: Create a new main.tf file in the root folder for any user of the module. In this file, you'll define the provider and reference the module.
```
provider "aws" {
    region = "us-east-1"
}

# Here instead of resource i will say is
module "ec2_instance" {
    source = "./modules/ec2_instance"     # where you have to fetch from you have to provide the path from the module
    ami_value = "ami-0fc5d935ebf8bc3bc"
    instance_type_value = "t2.micro"
}
```
#### Initialize Terraform:
```
terraform init
```
#### Plan the Terraform configuration:
```
terraform plan
```

#### Apply the Terraform configuration:
```
terraform apply
```

#### Review the Output:
```
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```
This setup allows for a clean and modular project structure where the module is defined in its dedicated folder (modules/ec2_instance), and the main configuration is kept separate for better organization and ease of use.


# Simplified Infrastructure with Terraform Modules

##  Using Modules for Reusability:
By organizing your Terraform code into modules, you're creating reusable and easy-to-maintain components. In your case, let's consider an example where you have an EC2 instance module.
```
/your_project
├── deployment.tf
└── /modules
    └── /ec2_instance
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```
The deployment.tf file in the root folder references the ec2_instance module, making it easy for anyone to use. This modular approach allows hundreds or thousands of team members to execute the project without diving into the complexities of the module itself.

## Expanding to Multiple Resources:
If you need to use multiple resources, say an EC2 instance and an S3 bucket, you can create separate modules for each.
```
/your_project
├── deployment.tf
└── /modules
    ├── /ec2_instance
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    ├── /s3_bucket
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
```
Now, users can use both modules in their deployment.tf file, providing the necessary values.

## Centralized Module Repository:
You can create a GitHub repository dedicated to Terraform modules. This can contain modules for various resources like VPCs, EKS clusters, etc.
```
/terraform-modules
├── /vpc
├── /eks
├── /ec2_instance
└── ...
```
Developers can easily access and use these modules in their projects by referencing the modules from this central repository.

## Private GitHub Repository for Modules:
If your organization prefers privacy and control over modules, you can create a private GitHub repository for your Terraform modules. This ensures that only authorized users within your organization can access and use these modules.

##### By adopting this approach, you provide developers with a straightforward way to use pre-built modules, and they only need to focus on their specific infrastructure needs by writing simple configuration files like deployment.tf. This leads to efficient and standardized infrastructure provisioning across the organization.
