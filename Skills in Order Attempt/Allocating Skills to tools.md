Pipe is the splitter so can split by newlines to create tally

Everything can usually be done in programming language / cli so our interest is everything outside of those

Main themes = debug - monitor, infrastructure changes, artifact creation, security, scaling, 

Timeline = events = architecture diagram

AWS exam guides for Developer

Domain 1: Development with AWS Services - 
Task Statement 1: Develop code for applications hosted on AWS.
Skills in:
• Creating fault-tolerant and resilient applications in a programming language (for example, Java, C#, Python, JavaScript, TypeScript, Go)
• Creating, extending, and maintaining APIs (for example, response/request transformations, enforcing validation rules, overriding status codes)
• Writing and running unit tests in development environments (for example, using AWS Serverless Application Model [AWS SAM])
• Writing code to use messaging services
• Writing code that interacts with AWS services by using APIs and AWS SDKs
• Handling data streaming by using AWS services
Task Statement 2: Develop code for AWS Lambda.
Skills in:
• Configuring Lambda functions by defining environment variables and parameters (for example, memory, concurrency, timeout, runtime, handler, layers, extensions, triggers, destinations)
• Handling the event lifecycle and errors by using code (for example, Lambda Destinations, dead-letter queues)
• Writing and running test code by using AWS services and tools
• Integrating Lambda functions with AWS services
• Tuning Lambda functions for optimal performance
Task Statement 3: Use data stores in application development.
Skills in:
• Serializing and deserializing data to provide persistence to a data store
• Using, managing, and maintaining data stores
• Managing data lifecycles
• Using data caching services

Domain 2: Security
Task Statement 1: Implement authentication and/or authorization for applications and AWS services.
Skills in:
• Using an identity provider to implement federated access (for example, Amazon Cognito, AWS Identity and Access Management [IAM])
• Securing applications by using bearer tokens
• Configuring programmatic access to AWS
• Making authenticated calls to AWS services
• Assuming an IAM role
• Defining permissions for principals
Task Statement 2: Implement encryption by using AWS services.
Skills in:
• Using encryption keys to encrypt or decrypt data
• Generating certificates and SSH keys for development purposes
• Using encryption across account boundaries
• Enabling and disabling key rotation
Task Statement 3: Manage sensitive data in application code.
Skills in:
• Encrypting environment variables that contain sensitive data
• Using secret management services to secure sensitive data
• Sanitizing sensitive data

Domain 3: Deployment
Task Statement 1: Prepare application artifacts to be deployed to AWS.
Skills in:
• Managing the dependencies of the code module (for example, environment variables, configuration files, container images) within the package
• Organizing files and a directory structure for application deployment
• Using code repositories in deployment environments
• Applying application requirements for resources (for example, memory, cores)
Task Statement 2: Test applications in development environments.
Skills in:
• Testing deployed code by using AWS services and tools
• Performing mock integration for APIs and resolving integration dependencies
• Testing applications by using development endpoints (for example, configuring stages in Amazon API Gateway)
• Deploying application stack updates to existing environments (for example, deploying an AWS SAM template to a different staging environment)
Task Statement 3: Automate deployment testing.
Skills in:
• Creating application test events (for example, JSON payloads for testing Lambda, API Gateway, AWS SAM resources)
• Deploying API resources to various environments
• Creating application environments that use approved versions for integration testing (for example, Lambda aliases, container image tags, AWS Amplify branches, AWS Copilot environments)
• Implementing and deploying infrastructure as code (IaC) templates (for example, AWS SAM templates, AWS CloudFormation templates)
• Managing environments in individual AWS services (for example, differentiating between development, test, and production in API Gateway)
Task Statement 4: Deploy code by using AWS CI/CD services.
Skills in:
• Updating existing IaC templates (for example, AWS SAM templates, CloudFormation templates)
• Managing application environments by using AWS services
• Deploying an application version by using deployment strategies
• Committing code to a repository to invoke build, test, and deployment actions
• Using orchestrated workflows to deploy code to different environments
• Performing application rollbacks by using existing deployment strategies
• Using labels and branches for version and release management
• Using existing runtime configurations to create dynamic deployments (for example, using staging variables from API Gateway in Lambda functions)

Domain 4: Troubleshooting and Optimization
Task Statement 1: Assist in a root cause analysis.
Skills in:
• Debugging code to identify defects
• Interpreting application metrics, logs, and traces
• Querying logs to find relevant data
• Implementing custom metrics (for example, CloudWatch embedded metric format [EMF])
• Reviewing application health by using dashboards and insights
• Troubleshooting deployment failures by using service output logs
Task Statement 2: Instrument code for observability.
Skills in:
• Implementing an effective logging strategy to record application behavior and state
• Implementing code that emits custom metrics
• Adding annotations for tracing services
• Implementing notification alerts for specific actions (for example, notifications about quota limits or deployment completions)
• Implementing tracing by using AWS services and tools
Task Statement 3: Optimize applications by using AWS services and features.
Skills in:
• Profiling application performance
• Determining minimum memory and compute power for an application
• Using subscription filter policies to optimize messaging
• Caching content based on request headers

AWS DevOps Engineer

Domain 1: SDLC Automation
Task Statement 1.1: Implement CI/CD pipelines.
Skills in:
• Configuring code, image, and artifact repositories
• Using version control to integrate pipelines with application environments
• Setting up build processes (for example, AWS CodeBuild)
• Managing build and deployment secrets (for example, AWS Secrets Manager, AWS Systems Manager Parameter Store)
• Determining appropriate deployment strategies (for example, AWS CodeDeploy)
Task Statement 1.2: Integrate automated testing into CI/CD pipelines.
Skills in:
• Running builds or tests when generating pull requests or code merges (for example, AWS CodeCommit, CodeBuild)
• Running load/stress tests, performance benchmarking, and application testing at scale
• Measuring application health based on application exit codes
• Automating unit tests and code coverage
• Invoking AWS services in a pipeline for testing
Task Statement 1.3: Build and manage artifacts.
Skills in:
• Creating and configuring artifact repositories (for example, AWS CodeArtifact, Amazon S3, Amazon Elastic Container Registry [Amazon ECR])
• Configuring build tools for generating artifacts (for example, CodeBuild, AWS Lambda)
• Automating Amazon EC2 instance and container image build processes (for example, EC2 Image Builder)
Task Statement 1.4: Implement deployment strategies for instance, container, and serverless environments.
Skills in:
• Configuring security permissions to allow access to artifact repositories (for example, AWS Identity and Access Management [IAM], CodeArtifact)
• Configuring deployment agents (for example, CodeDeploy agent)
• Troubleshooting deployment issues
• Using different deployment methods (for example, blue/green, canary)

Domain 2: Configuration Management and IaC
Task Statement 2.1: Define cloud infrastructure and reusable components to provision and manage systems throughout their lifecycle.
Skills in:
• Composing and deploying IaC templates (for example, AWS Serverless Application Model [AWS SAM], AWS CloudFormation, AWS Cloud Development Kit [AWS CDK])
• Applying CloudFormation StackSets across multiple accounts and AWS Regions
• Determining optimal configuration management services (for example, AWS OpsWorks, AWS Systems Manager, AWS Config, AWS AppConfig)
• Implementing infrastructure patterns, governance controls, and security standards into reusable IaC templates (for example, AWS Service Catalog, CloudFormation modules, AWS CDK)
Task Statement 2.2: Deploy automation to create, onboard, and secure AWS accounts in a multi-account or multi-Region environment.
Skills in:
• Standardizing and automating account provisioning and configuration
• Creating, consolidating, and centrally managing accounts (for example, AWS Organizations, AWS Control Tower)
• Applying IAM solutions for multi-account and complex organization structures (for example, SCPs, assuming roles)
• Implementing and developing governance and security controls at scale (AWS Config, AWS Control Tower, AWS Security Hub, Amazon Detective, Amazon GuardDuty, AWS Service Catalog, SCPs)

Task Statement 2.3: Design and build automated solutions for complex tasks and large-scale environments.
Skills in:
• Automating system inventory, configuration, and patch management (for example, Systems Manager, AWS Config)
• Developing Lambda function automations for complex scenarios (for example, AWS SDKs, Lambda, AWS Step Functions)
• Automating the configuration of software applications to the desired state (for example, OpsWorks, Systems Manager State Manager)
• Maintaining software compliance (for example, Systems Manager)

Domain 3: Resilient Cloud Solutions
Task Statement 3.1: Implement highly available solutions to meet resilience and business requirements.
Skills in:
• Translating business requirements into technical resiliency needs
• Identifying and remediating single points of failure in existing workloads
• Enabling cross-Region solutions where available (for example, Amazon DynamoDB, Amazon RDS, Amazon Route 53, Amazon S3, Amazon CloudFront)
• Configuring load balancing to support cross-AZ services
• Configuring applications and related services to support multiple Availability Zones and Regions while minimizing downtime
Task Statement 3.2: Implement solutions that are scalable to meet business requirements.
Skills in:
• Identifying and remediating scaling issues
• Identifying and implementing appropriate auto scaling, load balancing, and caching solutions
• Deploying container-based applications (for example, Amazon ECS, Amazon EKS)
• Deploying workloads in multiple Regions for global scalability
• Configuring serverless applications (for example, Amazon API Gateway, Lambda, AWS Fargate)
Task Statement 3.3: Implement automated recovery processes to meet RTO and RPO requirements.
Skills in:
• Testing failover of Multi-AZ and multi-Region workloads (for example, Amazon RDS, Amazon Aurora, Route 53, CloudFront)
• Identifying and implementing appropriate cross-Region backup and recovery strategies (for example, AWS Backup, Amazon S3, Systems Manager)
• Configuring a load balancer to recover from backend failure

Domain 4: Monitoring and Logging
Task Statement 4.1: Configure the collection, aggregation, and storage of logs and metrics.
Skills in:
• Securely storing and managing logs
• Creating CloudWatch metrics from log events by using metric filters
• Creating CloudWatch metric streams (for example, Amazon S3 or Amazon Kinesis Data Firehose options)
• Collecting custom metrics (for example, using the CloudWatch agent)
• Managing log storage lifecycles (for example, S3 lifecycles, CloudWatch log group retention)
• Processing log data by using CloudWatch log subscriptions (for example, Kinesis, Lambda, Amazon OpenSearch Service)
• Searching log data by using filter and pattern syntax or CloudWatch Logs Insights
• Configuring encryption of log data (for example, AWS KMS)
Task Statement 4.2: Audit, monitor, and analyze logs and metrics to detect issues.
Skills in:
• Building CloudWatch dashboards and Amazon QuickSight visualizations
• Associating CloudWatch alarms with CloudWatch metrics (standard and custom)
• Configuring AWS X-Ray for different services (for example, containers, API Gateway, Lambda)
• Analyzing real-time log streams (for example, using Kinesis Data Streams)
• Analyzing logs with AWS services (for example, Amazon Athena, CloudWatch Logs Insights)
Task Statement 4.3: Automate monitoring and event management of complex environments.
Skills in:
• Configuring solutions for auto scaling (for example, DynamoDB, EC2 Auto Scaling groups, RDS storage auto scaling, ECS capacity provider)
• Creating CloudWatch custom metrics and metric filters, alarms, and notifications (for example, Amazon SNS, Lambda)
• Configuring S3 events to process log files (for example, by using Lambda) and deliver log files to another destination (for example, OpenSearch Service, CloudWatch Logs)
• Configuring EventBridge to send notifications based on a particular event pattern
• Installing and configuring agents on EC2 instances (for example, AWS Systems Manager Agent [SSM Agent], CloudWatch agent)
• Configuring AWS Config rules to remediate issues
• Configuring health checks (for example, Route 53, ALB)

Domain 5: Incident and Event Response
Task Statement 5.1: Manage event sources to process, notify, and take action in response to events.
Skills in:
• Integrating AWS event sources (for example, AWS Health, EventBridge, CloudTrail)
• Building event processing workflows (for example, Amazon Simple Queue Service [Amazon SQS], Kinesis, Amazon SNS, Lambda, Step Functions)
Task Statement 5.2: Implement configuration changes in response to events.
Skills in:
• Applying configuration changes to systems
• Modifying infrastructure configurations in response to events
• Remediating a non-desired system state
Task Statement 5.3: Troubleshoot system and application failures.
Skills in:
• Analyzing failed deployments (for example, AWS CodePipeline, CodeBuild, CodeDeploy, CloudFormation, CloudWatch synthetic monitoring)
• Analyzing incidents regarding failed processes (for example, auto scaling, Amazon ECS, Amazon EKS)

Domain 6: Security and Compliance
Task Statement 6.1: Implement techniques for identity and access management at scale.
Skills in:
• Designing policies to enforce least privilege access
• Implementing role-based and attribute-based access control patterns
• Automating credential rotation for machine identities (for example, Secrets Manager)
• Managing permissions to control access to human and machine identities (for example, enabling multi-factor authentication [MFA], AWS Security Token Service [AWS STS], IAM profiles)
Task Statement 6.2: Apply automation for security controls and data protection.
Skills in:
• Automating the application of security controls in multi-account and multi-Region environments (for example, Security Hub, Organizations, AWS Control Tower, Systems Manager)
• Combining security controls to apply defense in depth (for example, AWS Certificate Manager [ACM], AWS WAF, AWS Config, AWS Config rules, Security Hub, GuardDuty, security groups, network ACLs, Amazon Detective, Network Firewall)
• Automating the discovery of sensitive data at scale (for example, Amazon Macie)
• Encrypting data in transit and data at rest (for example, AWS KMS, AWS CloudHSM, ACM)
Task Statement 6.3: Implement security monitoring and auditing solutions.
Skills in:
• Implementing robust security auditing
• Configuring alerting based on unexpected or anomalous security events
• Configuring service and application logging (for example, CloudTrail, CloudWatch Logs)
• Analyzing logs, metrics, and security findings
