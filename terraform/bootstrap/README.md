# Bootstrap Terraform

This directory contains **one-time setup** resources that must be applied **locally** 
with admin AWS credentials — NOT by the GitHub Actions CI/CD pipeline.

## Resources
- `github-oidc.tf` — Creates the GitHub OIDC provider and the `github-actions-twin-deploy` IAM role

## Why separate?
The GitHub Actions role cannot create its own prerequisites (circular dependency).
These resources must exist **before** any CI workflow can run.

## How to apply (run once, locally)

```bash
cd terraform/bootstrap
terraform init
terraform apply -var="github_repository=Sherifrax/digital-twin"
```

## ⚠️ Do NOT run terraform apply here from CI
This folder is intentionally excluded from the main `terraform/` CI apply.
