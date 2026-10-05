# 🚀 DevOps Internship – Task 3

## Infrastructure as Code (IaC) with Terraform

This project demonstrates **Infrastructure as Code (IaC)** using **Terraform** to provision a **local Docker container**.

Terraform is used to define and manage the Docker infrastructure through configuration files instead of creating the container manually.

---

## 🎯 Objective

The objective of this task is to:

* Understand Infrastructure as Code (IaC)
* Use Terraform to provision infrastructure
* Use the Docker provider with Terraform
* Create an Nginx Docker container using Terraform
* Understand Terraform `plan`, `apply`, `state`, and `destroy`
* Manage infrastructure using Terraform state

---

## 🛠️ Tools Used

* **Terraform**
* **Docker**
* **Nginx**
* **Git & GitHub**

---

## 📁 Project Structure

```text
devops-task-3-terraform/
│
├── main.tf
├── README.md
│
└── screenshots/
    ├── terraform-init.png
    ├── terraform-plan.png
    ├── terraform-apply.png
    ├── docker-container.png
    ├── nginx-browser.png
    └── terraform-destroy.png
```

---

## 🏗️ Architecture

```text
                Terraform
                    │
                    ▼
             Docker Provider
                    │
                    ▼
              Nginx Image
                    │
                    ▼
          Docker Container
          terraform-nginx
                    │
                    ▼
             Port Mapping
          localhost:8080
                    │
                    ▼
             Nginx Web Page
```

---

# 📄 Terraform Configuration

The infrastructure is defined in `main.tf`.

The Docker provider is used to communicate with the local Docker environment.

### Docker Image

Terraform pulls the Nginx Docker image:

```hcl
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

### Docker Container

Terraform creates a container named `terraform-nginx`:

```hcl
resource "docker_container" "nginx" {
  name  = "terraform-nginx"
  image = docker_image.nginx.image_id

  ports {
    internal = 80
    external = 80
  }
}
```

The application is therefore available at:

```text
http://localhost:80
```

---

# 🚀 Execution Steps

## 1. Check Terraform

```bash
terraform --version
```

## 2. Check Docker

```bash
docker --version
```

Make sure Docker Desktop is running.

---

## 3. Initialize Terraform

Initialize the Terraform working directory and download the required Docker provider.

```bash
terraform init
```

Expected result:

```text
Terraform has been successfully initialized!
```
---

## 4. Validate Terraform Configuration

Check whether the Terraform configuration is valid.

```bash
terraform validate
```

Expected result:

```text
Success! The configuration is valid.
```

---

## 5. Create Terraform Plan

The `terraform plan` command shows the changes Terraform intends to make without creating the resources.

```bash
terraform plan
```

Expected result:

```text
Plan: 2 to add, 0 to change, 0 to destroy.
```
---

## 6. Apply Terraform Configuration

Create the Docker image and container using Terraform.

```bash
terraform apply
```

When Terraform asks for confirmation, enter:

```text
yes
```

Expected result:

```text
Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```
---

# 🐳 7. Check Docker Container

Check the running Docker containers:

```bash
docker ps
```

The container should be visible:

```text
terraform-nginx
```
---

# 🌐 8. Access Nginx

Open the following URL in a browser:

```text
http://localhost:8080
```

The Nginx welcome page should be displayed.

---

# 📦 9. Check Terraform State

Terraform maintains information about the infrastructure in its state.

Run:

```bash
terraform state list
```

Expected resources:

```text
docker_container.nginx
docker_image.nginx
```

You can also view detailed state information:

```bash
terraform show
```

---

# 🗑️ 10. Destroy Infrastructure

Remove the infrastructure created by Terraform:

```bash
terraform destroy
```

Enter:

```text
yes
```

Expected result:

```text
Destroy complete! Resources: 2 destroyed.
```
---

# 🔄 Terraform Workflow

The complete Terraform workflow used in this task is:

```text
Write Terraform Configuration
          │
          ▼
   terraform init
          │
          ▼
  terraform validate
          │
          ▼
    terraform plan
          │
          ▼
   terraform apply
          │
          ▼
   Docker Container
          │
          ▼
 terraform state list
          │
          ▼
  terraform destroy
```

---

# 📚 Key Concepts Learned

### Infrastructure as Code (IaC)

Infrastructure as Code allows infrastructure to be defined and managed using configuration files.

### Terraform Provider

A provider allows Terraform to interact with an external platform.

In this project:

```text
Terraform → Docker Provider → Docker
```

### Terraform State

Terraform uses a state file to keep track of the infrastructure it manages.

```text
terraform.tfstate
```

### Terraform Plan

Shows the changes Terraform intends to make before applying them.

```bash
terraform plan
```

### Terraform Apply

Creates or updates the infrastructure.

```bash
terraform apply
```

### Terraform Destroy

Removes infrastructure managed by Terraform.

```bash
terraform destroy
```
---

# ✅ Task Outcome

By completing this task, I learned how to use **Terraform for Infrastructure as Code** and provision a **local Docker container** using the Docker provider.

I also learned the Terraform workflow:

```text
init → validate → plan → apply → state → destroy
```

---

## 📌 Task Submission

This repository contains:

* `main.tf`
* `README.md`
* Terraform execution screenshots
* Docker container verification
* Nginx application verification

```
