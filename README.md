# CI_DI_Jenkins_full

This repository provisions a complete CI/CD infrastructure using **Terraform** and automates security-focused deployments via **Jenkins**. It sets up a full DevSecOps pipeline, integrating tools for monitoring, secrets management, and application security scanning.

---

## 🚀 What This Code Does

The Terraform and Jenkins pipeline code in this repo:

- 🏗️ Provisions AWS infrastructure (EC2 instances, Security Groups, etc.)
- 🔐 Installs and configures **HashiCorp Vault** for secret management
- 🛡️ Installs **OWASP ZAP** and **Dastardly** for automated **DAST (Dynamic Application Security Testing)**
- 📊 Deploys **Grafana** and **Prometheus** for monitoring and observability
- 🧪 Sets up a secure Jenkins pipeline that:
  - Pulls code from a Git repository
  - Triggers DAST scans
  - Optionally runs additional SAST tools (can be extended)
  - Manages secrets via Vault
  - Logs and monitors pipeline health with Prometheus and Grafana
- ☁️ Configures outputs to display useful AWS metadata (e.g., IPs, DNS)

---

## 📁 Repository Structure

```bash
.
├── main.tf                # Terraform backend and provider config
├── servers.tf            # EC2 instances, Vault, Jenkins, monitoring stack
├── security-groups.tf    # AWS security group rules
├── outputs.tf            # Terraform output variables
├── variables.tf          # Input variables for customization
├── Jenkinfile            # Jenkins declarative pipeline script
├── scripts/              # Shell scripts to install and configure tools
│   ├── install-vault.sh
│   ├── install-zap.sh
│   ├── install-prometheus.sh
│   └── install-grafana.sh
└── .gitignore
```

---

## ✅ Prerequisites

- [Terraform](https://www.terraform.io/downloads.html)
- [Jenkins](https://www.jenkins.io/download/) installed (or provisioned by this code)
- AWS account with EC2 access
- AWS CLI configured (`aws configure`)

---

## ⚙️ Getting Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/derrickSh43/CI_DI_Jenkins_full.git
   cd CI_DI_Jenkins_full
   ```

2. **Initialize Terraform**:
   ```bash
   terraform init
   ```

3. **Plan infrastructure changes**:
   ```bash
   terraform plan
   ```

4. **Apply to deploy infrastructure**:
   ```bash
   terraform apply
   ```

5. **Access Jenkins**:
   - Use the public IP/DNS output from `terraform apply`
   - Log in and start the pipeline using the `Jenkinfile`

---

## 🧠 Notes

- Vault will be configured with a basic dev mode by default (can be hardened).
- OWASP ZAP and Dastardly are triggered as part of the Jenkins CI pipeline.
- Prometheus scrapes metrics from Jenkins and system targets.
- Grafana dashboards are automatically created (you can customize them).
- You can add more stages for things like Snyk, TruffleHog, or artifact promotion.

---

## 📜 License

MIT License — use freely, modify responsibly.
