# TASK: Infrastructure as Code (IaC) with Terraform

## 📌 Objective
Provision a **local Docker container** using **Terraform**.

----------------

## 🛠 Tools Used
- [Terraform](https://www.terraform.io/) – Infrastructure as Code (IaC) tool
- [Docker](https://www.docker.com/) – Container platform

--------------------

## 📂 Project Structure
terraform-docker/
│── main.tf # Terraform configuration file
│── README.md # Project documentation


## ⚙️ Setup Instructions

### 1️⃣ Prerequisites
- Docker installed and running  
  ```bash
  docker --version
   ```
- Terraform installed and which version it is.
 ```bash
terraform -version
 ```

2️⃣ Create main.tf
tf is the extension on terraform.
 ```bash
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {}

# Create Docker Image
resource "docker_image" "nginx_image" {
  name         = "nginx:latest"
  keep_locally = false
}

# Create Docker Container
resource "docker_container" "nginx_container" {
  name  = "my-nginx-container"
  image = docker_image.nginx_image.latest
  ports {
    internal = 80
    external = 8080
  }
}
 ```

## 🚀 Execution Steps
### Initialize Terraform
terraform init
### Preview the Plan
terraform plan
### Apply Configuration
terraform apply -auto-approve

This will:
Pull the latest nginx image.
Start a container mapping port 8080 → 80.

## Verify Container
docker ps
## Check Terraform State
terraform state list
## Destroy Infrastructure
terraform destroy -auto-approve
## 📜 Output
terraform apply -auto-approve

docker_image.nginx_image: Creating...

docker_image.nginx_image: Creation complete after 4s

docker_container.nginx_container: Creating...

docker_container.nginx_container: Creation complete after 2s

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
