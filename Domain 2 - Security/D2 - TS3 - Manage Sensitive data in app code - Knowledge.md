# Data classification (for example, personally identifiable information [PII], protected health information [PHI])

# Environment variables

# Secrets management (for example, AWS Secrets Manager, AWS Systems Manager Parameter Store)

## Secrets Manager

https://youtu.be/6oPHw7rT9OI - Back to Basics: Secrets Management - AWS

Store and Secure, audit and Rotation (uses lambda). Latest version of the secret, customer cmk, iam policies on secrets

https://youtu.be/Y3Gn_iP3FlE - Understanding AWS Secrets Manager - AWS Online Tech Talks - AWS Developer

PCI (?) requires 30 day rotation, Handson Demos

## Parameter Store

https://youtu.be/V10RcL0ONnU - How to secure and manage environment variables with Parameter Store in AWS - Pablos Spot

locals.tf, env and secret variables (lists) --> variables.tf, repos_json --> jsonencode, yaml decode and file commands. IAM resource in main.tf, resource "aws_ssm_parameter" "access"/"secret"/etc...  --> name type (SecureString) value, for each = local.secret variables - toset, value = UNSET, Lifecycle --> ignore changes  = [value]

# Secure credential handling

https://youtu.be/P1rsGaFoQ7U - How To Securely Store Your AWS Credentials in Terraform - Emmanuel Jijong

aws-vault another option
