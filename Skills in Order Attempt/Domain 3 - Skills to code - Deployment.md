***Domain 3: Deployment
Task Statement 1: Prepare application artifacts to be deployed to AWS.
Skills in:***

# Managing the dependencies of the code module (for example, environment variables, configuration files, container images) within the package

Here is an example of managing dependencies and assets for code modules in Python packages targeting AWS Lambda:

```python
import os
import boto3
from zipfile import ZipFile

# Package function code
with ZipFile('package.zip','w') as package:
  package.write('function.py')

  # Add config file to package
  config = """ 
API_KEY=12345678
LOG_LEVEL=info"""
  package.writestr('config.txt', config)

  # Add container image uri to env var
  env = {"IMAGES": "12345.dkr.ecr.us-east-1.amazonaws.com/myimage:latest"} 
  package.writestr('.env', str(env))

# Upload package 
s3 = boto3.client('s3')
s3.upload_file('package.zip', 'mybucket', 'package.zip')

# Reference package in CloudFormation
TEMPLATE = {
  "Resources": {
    "Function": {
      "Type": "AWS::Lambda::Function",
      "Properties": {
        "Code": {
          "S3Bucket": "mybucket",
          "S3Key": "package.zip"
        },
        "Environment": {
          "Variables": {
            "IMAGES": ".env:IMAGES"  
          }
        },
        "Handler": "function.handler",
        "Runtime": "python3.8"
      }
    }
  }  
}
```

The key points are:

- Package code with config files and env vars
- Reference env vars and packaged assets in AWS Lambda resource definition
- Env vars support S3 object reference syntax

Let me know if you have any other questions!

# Organizing files and a directory structure for application deployment

# Using code repositories in deployment environments

# Applying application requirements for resources (for example, memory, cores)

Here is an example of applying application resource requirements for an AWS Lambda function in Python:

```python
import boto3

lambda_client = boto3.client('lambda')

# Get existing lambda function
response = lambda_client.get_function(FunctionName='myFunction')

# Update memory and cores requirement
lambda_client.update_function_configuration(
    FunctionName='myFunction',
    MemorySize=512, # MB
    Timeout=60, # seconds
    Role=response['Configuration']['Role'],
    Runtime=response['Configuration']['Runtime'],
    Handler=response['Configuration']['Handler'],    
    Environment=response['Configuration']['Environment'],
    TracingConfig=response['Configuration']['TracingConfig']
)

print('Updated Lambda memory to 512MB and cores to 2')

# Updating cores 
lambda_client.update_function_configuration(
    FunctionName='myFunction',  
    ReservedConcurrentExecutions=100  
)

print('Updated reserved concurrency to 100!')
```

The key points are:

- Get existing config 
- Update MemorySize and ReservedConcurrentExecutions to set memory and cores
- Repass other config values

Let me know if you have any other questions!





Task Statement 2: Test applications in development environments.
Skills in:

# Testing deployed code by using AWS services and tools

Here is an example of testing deployed code on AWS Lambda using Python:

```python
import boto3
import json
import unittest

LAMBDA_NAME = "myLambda"

lambda_client = boto3.client('lambda')

class TestLambdaFunction(unittest.TestCase):

    def test_lambda_handler(self):
        test_payload = json.dumps({'key1': 'value1'})

        response = lambda_client.invoke(
            FunctionName=LAMBDA_NAME,
            Payload=test_payload
        )

        result = json.load(response['Payload'])

        # Assert output matches expected
        expected = {'key1': 'value1'}
        self.assertEqual(expected, result) 

if __name__ == '__main__':
    unittest.main()   
```

The key points for testing Lambda functions are:

- Use boto3 lambda client to invoke function 
- Pass test payload
- Validate output matches expected 

Can also test via Console, CloudWatch metrics/logs, X-Ray tracing etc.

Some other ways to test:

- Integration tests from EC2 calling function 
- Load tests using tools like Artillery

Let me know if you have any other questions!



# Performing mock integration for APIs and resolving integration dependencies

Here is an example of using mocks for API integration testing in Python and resolving dependencies:

**1. Define API Client**

```python
import requests

class OrdersAPI:
    def get_orders(user_id):
        resp = requests.get(f"https://api.orders.com/users/{user_id}/orders")
        return resp.json()

api = OrdersAPI()
```

**2. Create Mock Response**

```python
import pprint 
from unittest.mock import MagicMock

mock_response = [{'id': 1, 'total': 9.99}]
api.get_orders = MagicMock(return_value=mock_response)

resp = api.get_orders(user_id=123)
pprint.pprint(resp) # Prints mocked data
```

**3. Use Dependency Injection**

```python
def get_user_orders(api_client):
    user_id = get_user() 
    orders = api_client.get_orders(user_id)
    return orders

orders = get_user_orders(api=api) 
```

This allows using a simulated API client for testing to avoid hitting real services and isolate failures or latency. Dependency injection allows swapping the mock and real clients easily.

# Testing applications by using development endpoints (for example, configuring stages in Amazon API Gateway)

Here is an example of testing an application using development stages in Amazon API Gateway in Python:

**1. Deploy API to Dev Stage** 

Here is an example of using CloudFormation to deploy an API Gateway REST API to a dev stage in Python:

```python
import boto3

cf_client = boto3.client('cloudformation')

template = {
  "Resources": {
    "RestApi": {
      "Type": "AWS::ApiGateway::RestApi",
      "Properties": {
        "Name": "MyServiceDev",
        "EndpointConfiguration": {
          "Types": [
            "EDGE"
          ]  
        }
      }
    },
    "DevStage": {
     "Type": "AWS::ApiGateway::Stage",
     "Properties": {
        "RestApiId": {
          "Ref": "RestApi"
        }, 
        "StageName": "dev",
        "DeploymentId": {"Ref": "RestApiDeployment"}  
      }
    } 
  }
}

cf_client.create_stack(StackName="APIStack", TemplateBody=json.dumps(template))
```

This CloudFormation template creates a new REST API resource, and then a separate dev stage pointing at the latest deployment.

We can customize the stage variables, ACLs or API endpoint configuration specifically for the dev stage testing without impacting production configuration.

**2. Call Dev Stage Endpoint**

```python
import requests

dev_api_url = "https://abc123.execute-api.us-east-1.amazonaws.com/dev" 

headers = {'Authorization': 'token'}
data = {'param': 'value'}

resp = requests.post(dev_api_url, headers=headers, json=data)
print(resp.status_code)
print(resp.json())
```

**3. Configure Stage Variables**  

Allows testing different config like endpoints per stage.

**4. Mock Integration**

Use a mock integration pointing to a test Lambda function to test code in isolation.

**5. Switch to Prod**

Just change stage name when ready to route traffic to production.

This way the same API can be safely developed, tested and deployed incrementally without impacting end users. API Gateway stages allow isolating different versions till ready for primetime.

# Deploying application stack updates to existing environments (for example, deploying an AWS SAM template to a different staging environment)

Task Statement 3: Automate deployment testing.
Skills in:

# Creating application test events (for example, JSON payloads for testing Lambda, API Gateway, AWS SAM resources)

# Deploying API resources to various environments

Here is how you could deploy API resources to various environments in Python for AWS:

```python
import boto3

# Create API Gateway client
api_gateway = boto3.client('apigateway')

# Create the API
api = api_gateway.create_rest_api(
  name='myAPI',
  description='This is my API'
)
api_id = api['id']

# Create resource/methods in API
root_resource = api_gateway.get_resources(restApiId=api_id)['items'][0]
resource = api_gateway.create_resource(
  restApiId=api_id,
  parentId=root_resource['id'],
  pathPart='myResource'
)

api_gateway.put_method(
    restApiId=api_id,
    resourceId=resource['id'],  
    httpMethod='GET',
    authorizationType='NONE'
)

# Create stages for different environments 
stages = ['dev', 'test', 'prod']

for stage_name in stages:
  api_gateway.create_deployment(
    restApiId=api_id,
    stageName=stage_name
  )

print('API deployed to stages: {}'.format(stages))
```

This creates an API Gateway API, adds a /myResource resource with a GET method, and creates a deployment to dev, test, and prod stages to represent different environments.

Let me know if you need any clarification or have additional requirements to implement!

# Creating application environments that use approved versions for integration testing (for example, Lambda aliases, container image tags, AWS Amplify branches, AWS Copilot environments)

# Implementing and deploying infrastructure as code (IaC) templates (for example, AWS SAM templates, AWS CloudFormation templates)

Here is an example of implementing infrastructure as code (IaC) templates in Python using AWS SAM:

```python
import boto3
from botocore.exceptions import ClientError

TEMPLATE = """
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31    
Description: An AWS SAM template for a serverless application
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: python3.8
      CodeUri: s3://mybucket/functioncode.zip
"""

s3 = boto3.client('s3')

try:
  # Upload code artifact to S3
  s3.put_object(Bucket='mybucket', Key='functioncode.zip', Body=open('functioncode.zip', 'rb'))

  # Package SAM template
  cloudformation = boto3.client('cloudformation')
  response = cloudformation.package_and_deploy(
    Template=TEMPLATE,
    StackName='myStack',
    S3Bucket='mybucket',
    S3Prefix='sam-artifacts'
  )  

  # Print outputs
  print(response['StackId'])

except ClientError as e:
  print(e)  
```

This uploads a function code artifact to S3, packages the SAM template to upload needed artifacts to S3, deploys the CloudFormation stack, and prints the stack ID.

Let me know if you need any help with implementing other IaC templates or frameworks!

# Managing environments in individual AWS services (for example, differentiating between development, test, and production in API Gateway)

Task Statement 4: Deploy code by using AWS CI/CD services.
Skills in:

# Updating existing IaC templates (for example, AWS SAM templates, CloudFormation templates)

Here is an example of how to update an existing AWS SAM template in Python:

```python
import boto3

# Existing SAM template
TEMPLATE = {
  "Resources": {
    "MyFunction": {
      "Type": "AWS::Serverless::Function",
      "Properties": {
        "Runtime": "python3.8",
        "Handler": "index.handler",
        "CodeUri": "s3://mybucket/functioncode.zip"  
      }
    }
  }
}

cloudformation = boto3.client('cloudformation')

# Make updates to template
TEMPLATE["Resources"]["MyFunction"]["Properties"]["Runtime"] = "python3.9" 

try:
  # Package updated template
  response = cloudformation.package_and_deploy(
    Template=TEMPLATE,
    StackName='myStack',
    S3Bucket='mybucket',
    Capabilities=["CAPABILITY_IAM"],
    ForceUpdate=True # update existing stack
  )

  print(response['StackId'])

except Exception as e:
  print(e)
```

The key points are:

- Load existing template
- Make updates 
- Package and redeploy using `ForceUpdate=True` to update existing stack

Some other ways to update:

- Use separate update_stack() call instead of package_and_deploy()
- Use change sets to preview changes before applying

Let me know if you have any other questions!

# Managing application environments by using AWS services

Here is an example of managing application environments in Python using AWS services:

```python
import boto3
from botocore.exceptions import ClientError

# Create Environment Resource Tags
dev_tags = [{'Key': 'env', 'Value': 'dev'}]
prod_tags = [{'Key': 'env', 'Value': 'prod'}]

# Lambda Function 
lambda_client = boto3.client('lambda')

def create_function(name, role, tags):
  try:
    lambda_client.create_function(
      FunctionName=name,
      Runtime='python3.8',  
      Role=role,
      Handler='lambda_function.lambda_handler',
      Code={'ZipFile': open('function.zip', 'rb')},
      Tags=tags    
    )
  except ClientError as e:
    print(e)


create_function('myfunction-dev', 'arn:aws:iam::123456789012:role/lambda-role', dev_tags)  

create_function('myfunction-prod', 'arn:aws:iam::123456789012:role/lambda-role', prod_tags)

# API Gateway REST API
api_client = boto3.client('apigateway') 

def create_api(name, tags):
  try:  
    rest_api = api_client.create_rest_api(
      name=name,
      tags=tags
    )  
    return rest_api['id']
  except ClientError as e:
    print(e)


dev_api = create_api('myapi-dev', dev_tags)
prod_api = create_api('myapi-prod', prod_tags)

print('Application environments created!')
```

The key ideas are:

- Tag resources with env=dev/prod
- Modular functions to create environments 
- Separate dev/prod APIs 

Let me know if you have any other questions!

# Deploying an application version by using deployment strategies

# Committing code to a repository to invoke build, test, and deployment actions

Here is an example workflow for committing code to a GitHub repository to trigger build, test, and deployment actions using AWS services:

```python
import boto3 
from github import Github

# Connect to GitHub 
gh = Github(AWS_KEY)
repo = gh.get_repo("myorganization/myrepo")

# Make code changes
contents = repo.get_contents("src/function.py")
repo.update_file(contents.path, "Updates function", contents.decoded_content, contents.sha)

# Commit to master branch
commit_message = "Update function"
master_ref = repo.get_git_ref('heads/master') 
master_sha = master_ref.object.sha  
base_tree = repo.get_git_tree(master_sha)
new_tree = repo.create_git_tree([contents])
commit = repo.create_git_commit(commit_message, new_tree, [master_sha])
master_ref.edit(commit.sha)
print("Committed to GitHub!")

# GitHub Actions workflow triggered on push
# Build, test, deploy function to AWS Lambda

# Validate deployment
test_lambda(LAMBDA_NAME)
```

Key points:

- Update files in GitHub repo 
- Commit changes to master branch 
- GitHub Actions workflow handles build, test, deploy
- Test deployed Lambda function

Let me know if you have any other questions!

# Using orchestrated workflows to deploy code to different environments

# Performing application rollbacks by using existing deployment strategies

Here is an example of performing an application rollback on AWS Lambda using aliases and weighted aliases:

```python
import boto3

lambda_client = boto3.client('lambda')  

# Production version
prod_version = lambda_client.publish_version(FunctionName='myFunction')['Version']

# Create alias for prod  
lambda_client.create_alias(
  Name='prod',
  FunctionName='myFunction',
  FunctionVersion=prod_version  
)

# New version deployed to alias
new_version = lambda_client.publish_version(FunctionName='myFunction')['Version'] 

# Assign all traffic to new version
lambda_client.update_alias(
  Name='prod',
  FunctionName='myFunction',
  FunctionVersion=new_version  
)

# Something went wrong! Rollback...

# Reassign previous prod version
lambda_client.update_alias(
  Name='prod',
  FunctionName='myFunction',
  FunctionVersion=prod_version
)

# Validate prod alias points to previous version
prod_info = lambda_client.get_alias(Name='prod')

print(f"Rollbacked version: {prod_info['FunctionVersion']}")
```

Key points:

- Use aliases to manage function versions
- Re-point alias to previous version for quick rollback  

Let me know if you have any other questions!

# Using labels and branches for version and release management

Here is an example of using labels and branches for version and release management with GitHub and AWS Lambda:

```python
import boto3
from github import Github

gh = Github(GITHUB_TOKEN)
repo = gh.get_repo("myorg/myrepo")

lambda_client = boto3.client('lambda')

# New version branch
branch_name = "version-1.1" 
repo.create_git_ref(f"refs/heads/{branch_name}", repo.get_branches()[0].commit.sha)

# Make changes
contents = repo.get_contents("function.py", ref=branch_name)
repo.update_file(contents.path, "v1.1 updates", contents.decoded_content, contents.sha, branch=branch_name)

# Commit and push changes  
repo.get_branch(branch_name).commit.create_file(path="testing.txt", content="testing")

# Create release tag
release = repo.create_git_release(f"v1.1", branch_name, "Version 1.1", target_commitish=branch_name)
release.update_release(name="v1.1", message="Version 1.1", draft=False)  

# Deploy tagged version to Lambda alias
lambda_client.publish_version(FunctionName="myFunction")  
version = lambda_client.get_function(FunctionName="myFunction")["Configuration"]["Version"]
lambda_client.create_alias(Name="v1.1", FunctionName="myFunction", FunctionVersion=version)
```

Key points:

- Use branches for new versions
- Commit changes and tag releases on branches
- Deploy tagged release to a Lambda alias

Let me know if you have any other questions!

# Using existing runtime configurations to create dynamic deployments (for example, using staging variables from API Gateway in Lambda functions)

Here is an example of using API Gateway stage variables to create a dynamic deployment of a Lambda function in Python:

```python
import boto3

api_client = boto3.client('apigateway')
lambda_client = boto3.client('lambda')

# Create stage variable in API Gateway
api_client.create_stage(
  restApiId='abcdef123',
  stageName='dev',
  deploymentId='123abc',
  variables={
    "environment": "dev"
  }
)

# Lambda function to process request
def lambda_handler(event, context):
  env = event['stageVariables']['environment'] 
  print(f"The environment is: {env}")

  # Environment specific logic
  if env == 'dev':
    return dev_response() 
  elif env == 'prod':  
    return prod_response()

# Upload lambda function code 

# Create lambda function  
lambda_client.create_function(
  FunctionName='myFunction',
  # other params...
  Environment={
    'Variables': {
      # Pass stage variable to lambda  
      "ENV": "$stageVariables.environment"
    }
  }  
)

# Permission to API Gateway to invoke lambda
lambda_client.add_permission(# permission params)

# Redeploy API    
api_client.create_deployment(
  restApiId='abcdef123', 
  stageName='dev'
)

print("Dynamic deployment complete!")
```

Key points:

- Define stage variables in API Gateway
- Pass variables to Lambda via env vars
- Redeploy API to apply config changes

Let me know if you have any other questions!
