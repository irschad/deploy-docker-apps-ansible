# Ansible & Docker Project

## Project Overview
This project demonstrates the automation of Docker application deployment on an AWS EC2 instance. The workflow involves using Terraform to provision the infrastructure, Ansible to configure the server and deploy Docker, and Docker Compose to manage application containers.

---

## Technologies Used

- **Ansible**: Configuration management and automation.
- **AWS**: Cloud infrastructure provider.
- **Docker**: Containerization platform.
- **Terraform**: Infrastructure as Code (IaC) tool.
- **Linux**: Operating system for server setup.

---

## Project Description

1. **Infrastructure Setup:** Use Terraform to provision an AWS EC2 instance.
2. **Server Configuration:** Use Ansible to:
   - Install Docker and Docker Compose.
   - Configure user permissions for Docker.
   - Deploy a `docker-compose` file to the server.
   - Start the Docker containers defined in the `docker-compose` file.

---

## Steps to Recreate the Project

### 1. Provision AWS EC2 Instance with Terraform

#### Preparation
- Ensure you have Terraform installed.
- Configure AWS CLI credentials for Terraform to use.
- Create a directory called `terraform` and include the following files:
  - `main.tf`
  - `providers.tf`
  - `terraform.tfvars`

#### Commands to Execute
```bash
cd terraform
terraform init
terraform apply --auto-approve
```
Upon successful execution, the EC2 instance's public IP will be displayed as output.

---

### 2. Configure the Server with Ansible

#### Preparation
1. Add the following files to the project directory:
   - `ansible.cfg`:
     ```ini
     [defaults]
     inventory = ./hosts
     host_key_checking = False
     ```
   - `hosts`:
     ```ini
     [docker_server]
     <EC2_PUBLIC_IP> ansible_user=ec2-user ansible_python_interpreter=/usr/bin/python3 ansible_ssh_private_key_file=~/.ssh/id_ed25519
     ```
   - `deploy-docker-ec2-user.yaml` and/or `deploy-docker-new-user.yaml`: Contains the Ansible Playbooks for Docker setup and container deployment.
   - `project-vars`:
     ```yaml
     docker_password: "your_dockerhub_password"
     ```

#### Commands to Execute
Run the Ansible Playbook:
```bash
cd ansible
ansible-playbook deploy-docker-ec2-user.yaml
```
For the new user:
```bash
ansible-playbook deploy-docker-new-user.yaml
```
---

### 3. Docker Compose File

The `docker-compose-full.yaml` file contains definitions for the following services:

- **Java Application**: A containerized Java application.
- **MySQL Database**: MySQL server for data persistence.
- **phpMyAdmin**: GUI for managing the MySQL database.

---

### 4. Start Docker Containers

The Playbook will automatically:
- Log in to Docker Hub.
- Deploy and start the containers based on the `docker-compose.yaml` file.

---

## Project Files

- **Terraform Files:**
  - `main.tf`, `providers.tf`, and `terraform.tfvars` for infrastructure provisioning.
- **Ansible Playbooks:**
  - `deploy-docker-ec2-user.yaml`: Configures Docker for `ec2-user`.
  - `deploy-docker-new-user.yaml`: Configures Docker for a newly created user.
- **Docker Compose File:**
  - `docker-compose-full.yaml`: Defines the services for deployment.
- **Configuration Files:**
  - `ansible.cfg` and `hosts`: Ansible configuration.

---

## Outputs

Upon successful execution:
- The EC2 instance will have Docker and Docker Compose installed.
- Docker containers for the Java app, MySQL, and phpMyAdmin will be running.
- Access the services via the public IP of the EC2 instance.


---

## Conclusion
This project demonstrates the end-to-end automation of infrastructure provisioning, server configuration, and application deployment using Terraform, Ansible, and Docker. It highlights the power of combining Infrastructure as Code with configuration management tools to simplify complex deployment workflows.

