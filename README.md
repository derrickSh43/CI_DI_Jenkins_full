# CI/CD Jenkins Automation with Terraform 🚀

This project provisions a complete CI/CD pipeline using **Jenkins**, fully automated through **Terraform** and shell scripts. It showcases Infrastructure as Code (IaC), continuous integration, and automated deployment to a Tomcat server—all hosted on AWS EC2.

---

## 📌 Key Features

- ✅ Automated provisioning of Jenkins CI/CD infrastructure on AWS using Terraform
- ✅ EC2 instances with security groups, SSH access, and networking setup
- ✅ Auto-installation of Jenkins, Java, Git, Maven, and Tomcat via user data scripts
- ✅ Jenkins pipeline (`Jenkinfile`) for:
  - Cloning a GitHub project
  - Building with Maven
  - Deploying to Tomcat
- ✅ Easy to extend for production-grade pipelines

---

## 🧱 Architecture

```
Terraform → AWS EC2 (Ubuntu) → User Data Scripts → Jenkins Master
                                            ↳ Optional Jenkins Agent
                                            ↳ Deploy to Tomcat Server
```

- **Jenkins Master**: Installed and configured automatically
- **Tomcat Server**: Receives deployed builds from Jenkins
- **Security Groups**: Allow secure access to services (port 22, 8080, 8081)

---

## 🚀 Deployment Steps

### Prerequisites

- AWS CLI configured
- Terraform installed
- SSH key pair (saved locally)
- GitHub personal access token (optional, if accessing private repos)

---

### 1. Clone the Repository

```bash
git clone https://github.com/derrickSh43/CI_DI_Jenkins_full.git
cd CI_DI_Jenkins_full
```

---

### 2. Customize Variables

Update values in `terraform.tfvars` (optional) or inline inside `main.tf` if applicable:
- AWS region
- Key pair name
- Instance type
- GitHub repo (in `Jenkinfile`)

---

### 3. Initialize and Apply Terraform

```bash
terraform init
terraform apply -auto-approve
```

This spins up:
- EC2 instances (Jenkins master, Tomcat)
- Security groups
- Networking configuration

---

### 4. Access Jenkins

- Get the public IP of your Jenkins EC2 instance:
  ```bash
  terraform output jenkins_ip
  ```
- Visit `http://<jenkins_ip>:8080`
- Retrieve Jenkins admin password from `/var/lib/jenkins/secrets/initialAdminPassword` (SSH into instance)

---

### 🛠️ Jenkins Pipeline

The pipeline is defined in `Jenkinfile` and performs the following:
- Pulls source code from GitHub
- Builds using Maven
- Deploys `.war` file to the Tomcat server

Modify the `Jenkinfile` as needed to match your repo and deployment process.

---

## 📦 Project Structure

```
.
├── scripts/
│   ├── install_jenkins.sh
│   ├── install_java.sh
│   ├── install_tomcat.sh
├── Jenkinfile
├── main.tf
├── outputs.tf
├── servers.tf
├── security-groups.tf
└── variables.tf
```

---

## 📈 Future Enhancements

- [ ] Add monitoring with Prometheus + Grafana or CloudWatch
- [ ] Store Jenkins artifacts in S3 or Artifactory
- [ ] Implement rollback using Jenkins pipeline logic
- [ ] Modularize Terraform for easier reusability
- [ ] Replace SSH keypair with AWS Session Manager
- [ ] Add CI/CD for infrastructure (Terraform Cloud or Atlantis)

---

## 🧠 Author
  
Cloud Engineer | CI/CD & DevOps Specialist  
GitHub: [@derrickSh43](https://github.com/derrickSh43)

---

## 🛡️ License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
