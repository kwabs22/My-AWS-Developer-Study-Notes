# Identity federation (for example, Security Assertion Markup Language [SAML], OpenID Connect [OIDC], Amazon Cognito)

# AND

# The comparison of user pools and identity pools in Amazon Cognito

## Security Assertion Markup Language

https://youtu.be/bmZdZy6qe24 - SAML | What is SAML | Intro to Security Assertion Markup Language | Intellipaat - Intellipaat

XML Based metadata file , IDP with Auth0 and Service Provider

## OpenID Connect

https://youtu.be/A7GVeqFvqFM - SAML vs. OpenID (OIDC): What's the Difference? - JumpCloud

OpenID based on OAuth2, SSO connectors

## Cognito

https://youtu.be/QEGo6ZoN-ao - Amazon Cognito Beginner Guide - Be a Better Dev

supports upto 40 million users, supports OAuth2.0, SAML and OIDC, Cognito can be the IDP but SSO will also add from IDP to cognito, userpool hosted UI, Application Integration - API Gateway / Amplify / SDK, Triggers for cognito events, Identity Pools can select IAM roles for users, token based assignment and claims, policy based

# Bearer tokens (for example, JSON Web Token [JWT], OAuth, AWS Security Token Service [AWS STS])

## JWT

https://youtu.be/UBUNrFtufWo - Session vs Token Authentication in 100 Seconds - Fireship

Client vs Server created tokens

## OAuth

https://youtu.be/ZV5yTm4pT8g - OAuth 2 Explained In Simple Terms - ByteByteGo

## AWS STS

https://youtu.be/hYBxwzmJb5w - IAM — AWS Security Token Service (STS) - ExamPro

https://youtu.be/uK_mIbhp-H4 - IAM — AssumeRoleWithWebIdentity - ExamPro

OAuth to Facebook provides JWT we send to AssumeRoleWithWebIdentity and it decides to give temp IAM token 

# Resource-based policies, service policies, and principal policies

https://youtu.be/Y3Gn_iP3FlE - Understanding AWS Secrets Manager - AWS Online Tech Talks - AWS Developer

Resource-based at 8:00, Principal (if meaning user) - tag-based at 7:20

# Role-based access control (RBAC)

https://youtu.be/4Uya_I_Oxjk - Role-Based Access Control (RBAC) Explained: How it works and when to use it - Erik Wilde

Access Management, Permissions (role has multiple permissions) and capabilities (permission can have multiple capabilities), roles and users (can have multiple roles - scalability), ACL is simpler (smaller in scope)

# Application authorization that uses ACLs

# AND

# The principle of least privilege

https://youtu.be/6zi75JUXB94 - Authorization | RBAC and ACLs | Confluent Cloud Security - Confluent (Managed Kafka as a Service)

Tables with identities and what they can do, specific to resources

# Differences between AWS managed policies and customer-managed policies

# Identity and access management
