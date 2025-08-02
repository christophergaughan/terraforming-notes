# Terraforming Notes 🪐

This repository contains clean, modular, and well-documented Terraform examples and references. It serves as a working knowledge base for Infrastructure-as-Code (IaC) using Terraform across AWS and cloud-native environments.

## 📦 Repository Structure

```
.
├── notes/                  # Markdown notes explaining Terraform concepts
│   ├── 01_providers.md
│   ├── 02_resources.md
│   └── 03_variables_outputs.md
├── sandbox/                # Hands-on Terraform experiments
│   └── s3-versioning/
│       └── main.tf
└── README.md
```

## Key Terraform Concepts

Each note is paired with runnable `.tf` files. Topics covered include:

- **Providers**  
  Configure cloud APIs and authentication.  
  → Example: `aws`, `google`, `github`

- **Resources**  
  Define real infrastructure — like EC2 instances, S3 buckets, and Lambda functions.

- **Variables & Outputs**  
  Parameterize infrastructure and expose key data to other modules or users.

- **State Management**  
  Track changes to infrastructure over time using local or remote backends.

- **Modules** *(coming soon)*  
  Reusable Terraform components for DRY, scalable architecture.

## Example: S3 Bucket with Versioning

📁 [`sandbox/s3-versioning/main.tf`](sandbox/s3-versioning/main.tf)

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "versioned_bucket" {
  bucket = "example-versioned-bucket-${random_id.bucket_id.hex}"
  acl    = "private"

  versioning {
    enabled = true
  }

  tags = {
    Name        = "Versioned Bucket"
    Environment = "Dev"
  }
}

resource "random_id" "bucket_id" {
  byte_length = 4
}
```

## How to Run Any Example

```
cd sandbox/<folder-name>
terraform init
terraform plan
terraform apply
```

## 🧠 Why This Repo?

This repo is intended for:
- Cloud engineers building IaC skills
- MLOps and platform engineers integrating with Terraform
- Anyone looking for real, runnable `.tf` code with no fluff

## Roadmap

- [ ] Add module examples
- [ ] Add remote backend config examples
- [ ] Add GitHub Actions CI/CD example for Terraform
- [ ] Add IAM and security-focused Terraform configurations

## 📜 License

MIT License
