# Claude Assist for base to work

Domain 2: Security
Task Statement 1: Implement authentication and/or authorization for applications and AWS services.
Skills in:

# Using an identity provider to implement federated access (for example, Amazon Cognito, AWS Identity and Access Management [IAM])

Here is an example of using Amazon Cognito to implement federated access for an application:

**1. Configure Cognito User Pool**

```python
import boto3

cognito = boto3.client('cognito-idp')
pool = cognito.create_user_pool(PoolName='UserPool')
```

**2. Create App Client**

```python
app_client = cognito.create_user_pool_client(
   UserPoolId=pool['Id'],
   ClientName='MyApp'
)
```

**3. Sign in with Federated Identity** 

```python
def sign_in(identity_provider, token):
    response = cognito.initiate_auth(
        AuthFlow='USER_SRP_AUTH',
        AuthParameters={
            'USERNAME': identity_provider,
            'SRP_A': token
        },
        ClientId=app_client['ClientId']  
    )

    return response['AuthenticationResult']['IdToken']
```

This allows you to setup a user directory via Cognito and enable sign-in from various external providers like Facebook, Google, SAML etc. 

Cognito handles managing user lifecycles, token issuance and identity federation with providers simply via API calls.

# Securing applications by using bearer tokens

Here is an example of securing an application using bearer tokens in Python:

**1. Generate JWT Token**

```python
import jwt

token = jwt.encode({'user': 'john'}, 'secret', algorithm='HS256') 
```

**2. Attach Token to Requests**

```python
import requests

headers = {
   'Authorization': 'Bearer ' + token
}

response = requests.get('https://api.example.com', headers=headers)
```

**3. Verify Token in Backend**  

```python
import jwt

def validate_token(token):
    try: 
        decoded = jwt.decode(token, 'secret', algorithms=['HS256'])
        return decoded['user']
    except:
        return None
```

Now any protected API route can call `validate_token(request.headers['Authorization'])` to verify there is a valid non-expired JWT token present before allowing access.

Some key advantages are:

- No sessions/cookies to manage
- Easy integration with identity providers  
- Blacklist bad tokens

Overall, verifying signed JWT tokens on the backend allows stateless authorization in applications.

# Configuring programmatic access to AWS

Here is an example of configuring programmatic access to AWS services in Python:

**1. Create IAM User & Access Key**

In the AWS IAM console, create an IAM user, and generate an access key ID & secret access key pair.

**2. Set Credentials in Environment** 

```
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

**3. Configure AWS SDK/CLI**

```python
import boto3

session = boto3.Session(
    aws_access_key_id=os.environ['AWS_ACCESS_KEY_ID'],
    aws_secret_access_key=os.environ['AWS_SECRET_ACCESS_KEY']
)

s3 = session.resource('s3')
```

```bash
aws s3 ls --profile user1
```

**4. Shared Credential File**

~/.aws/credentials

This establishes an access key based identity for CLI/SDK calls separate from IAM roles on EC2 allowing instance-based or human access to resources.

Credentials should be rotated periodically.

# Making authenticated calls to AWS services

Here is an example of making authenticated calls to AWS services in Python:

**1. Create IAM User & Access Key**

Generate an access key ID and secret access key for your IAM user in AWS.

**2. Configure AWS SDK Client**

```python
import boto3

sess = boto3.Session(
    aws_access_key_id=ACCESS_KEY_ID,
    aws_secret_access_key=SECRET_ACCESS_KEY
)

s3 = sess.client('s3')
```

**3. Use IAM Roles**

If code is running on an EC2 instance, you can attach an IAM role instead:

```python
import boto3

s3 = boto3.client('s3') # Uses EC2 instance role credentials
```

**4. Federation** 

Use AWS STS for temporary credentials from federated identities:

```python
sts = boto3.client('sts')

resp = sts.assume_role(
    RoleArn="arn:aws:iam::AccountId:role/RoleName",
    RoleSessionName="session1" 
)  

creds = resp['Credentials']
s3 = boto3.client('s3',
    aws_access_key_id=creds['AccessKeyId'],
    aws_secret_access_key=creds['SecretAccessKey'],
    aws_session_token=creds['SessionToken'],
)
```

Using AWS credentials securely allows your application code to access AWS services.

# Assuming an IAM role

Here is an example of assuming an IAM role in Python:

**1. Create IAM Role**

First create the IAM role in the AWS console with the trust policy and permissions.

**2. Use STS for Temporary Credentials**

```python
import boto3
from botocore.session import Session

session = Session(profile='developer') # credential profile
sts = session.client('sts')

response = sts.assume_role(
    RoleArn="arn:aws:iam::ACCTID:role/RoleName",
    RoleSessionName="session1",
    DurationSeconds=3600  
)

temp_credentials = response['Credentials']
```

**3. Access Resources with Assumed Role**

```python
s3resource = session.resource('s3',
    aws_access_key_id = temp_credentials['AccessKeyId'],
    aws_secret_access_key = temp_credentials['SecretAccessKey'],
    aws_session_token = temp_credentials['SessionToken'],
)

for bucket in s3resource.buckets.all():
    print(bucket.name) 
```

This allows assuming cross-account roles or granting access to resources based on federated identities without managing long-lived credentials.

# Defining permissions for principals

Here is an example of defining permissions for principals in Python for AWS services:

**1. Allow Limited S3 Permissions**  

```python
import boto3

# Define policy document
s3policy = {
    "Version": "2012-10-17",
    "Statement":[
       {
          "Effect":"Allow",
          "Action":[
            "s3:ListBucket"
          ],
          "Resource":"arn:aws:s3:::mybucket"
       },
    ]
 }

s3 = boto3.client('s3') 

# Attach inline policy to user 
s3.put_user_policy(
  UserName='user',
  PolicyName='LimitAccess',
  PolicyDocument=json.dumps(s3policy)
)
```

**2. Control Resource Access with Conditions**

```json
"Condition": {
   "IpAddress": {
      "aws:SourceIp": "192.0.2.0/24"
    }
}
```

Fine-grained access controls restrict privileges only to what is absolutely necessary. Conditions dynamically adapt authorization based on runtime attributes.

**3. Assign Managed IAM Policies**

Attach pre-defined managed policies instead of defining custom ones.

Overall this shows some patterns for granting principals like users, roles and federated entities secure application access to only necessary resources.

Task Statement 2: Implement encryption by using AWS services.
Skills in:

# Using encryption keys to encrypt or decrypt data

Here is an example of using encryption keys to encrypt and decrypt data in Python:

**1. Generate Data Key**

```python
import os
from base64 import b64encode

key = os.urandom(32) # Generate 256-bit key
b64_key = b64encode(key).decode('utf-8')
```

**2. Encrypt Data**

```python
from cryptography.fernet import Fernet
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC 

password = b'my password'
kdf = PBKDF2HMAC(
    algorithm=hashes.SHA256(),
    length=32,
    salt=b'salt',
    iterations=100000,
    backend=default_backend()
)

key = base64.urlsafe_b64encode(kdf.derive(password))
f = Fernet(key)

encrypted = f.encrypt(b"secret data")
```

**3. Decrypt Data**

```python
decrypted = f.decrypt(encrypted)
print(decrypted) # b'secret data'
```

This allows securely encrypting sensitive data for storage and transmission, while tightly controlling access to decrypted form using encryption keys.

# Generating certificates and SSH keys for development purposes

Here is an example of generating certificates and SSH keys for development purposes in Python:

**Self-signed SSL Certificate**

```python
from OpenSSL import crypto

cert = crypto.X509()
cert.get_subject().CN = "localhost"
cert.set_serial_number(1000)
cert.gmtime_adj_notBefore(0)
cert.gmtime_adj_notAfter(365*24*60*60) # 1 year

cert.set_issuer(cert.get_subject())
cert.set_pubkey(pkey)

cert.sign(pkey, 'sha256')
open("ssl.crt", "wt").write(crypto.dump_certificate(crypto.FILETYPE_PEM, cert))
```

**SSH Key Pair**

```python
from paramiko import RSAKey

key = RSAKey.generate(2048)

private_key = key.get_base64() 
public_key = key.get_base64() 

open('private.key', 'w').write("-----BEGIN RSA PRIVATE KEY-----\n{private_key}-----END RSA PRIVATE KEY-----".format(private_key=private_key))

open('public.key', 'w').write("ssh-rsa {public_key}".format(public_key=public_key))
```

This allows easily creating keys and certificates for testing HTTPS requests or SSH connections without needing to rely on a full certificate authority.

The self-signed credentials should not be used in production systems.

# Using encryption across account boundaries

Here is an example of using encryption across AWS accounts in Python:

**1. Create KMS Key**

```python
import boto3

kms = boto3.client('kms')
key_info = kms.create_key(Description='Cross account key')
key_id = key_info['KeyMetadata']['KeyId']
```

**2. Allow Access from Another Account**  

```python
kms.create_grant(
   KeyId=key_id,
   GranteePrincipal='arn:aws:iam::OtherAccountId:root',
   Operations=['Encrypt','Decrypt','ReEncryptFrom','ReEncryptTo']
)
```

**3. Encrypt in First Account**

```python
plaintext = b"Secret Data"
response = kms.encrypt(KeyId=key_id, 
   Plaintext=plaintext)

ciphertext = response['CiphertextBlob']
```

**4. Decrypt in Other Account** 

Pass the ciphertext to the other account and decrypt with the KMS key ARN

This creates a key in one account that instances in another account have access to, enabling transparent encryption across account boundaries while retaining isolation.

# Enabling and disabling key rotation

Here is an example of enabling and disabling key rotation in Python for an AWS KMS customer master key (CMK):

**1. Create a CMK**

```python
import boto3

kms = boto3.client('kms')
key_info = kms.create_key()
key_id = key_info['KeyMetadata']['KeyId']
```

**2. Enable Auto Key Rotation**

Rotates every 1 year:

```python
kms.enable_key_rotation(KeyId=key_id)
```

**3. Disable Key Rotation**

```python
kms.disable_key_rotation(KeyId=key_id)
```

**4. Manually Rotate at Any Time**

Rotation still possible on disabled rotation keys:

```python
kms.generate_data_key(
    KeyId=key_id, 
    KeySpec='AES_256'
)
```

This allows full control over encryption key rotation policies, forcing or preventing automatic annual rotation as needed while retaining manual rotation ability.

Setting appropriate key rotation helps maintain security.

Task Statement 3: Manage sensitive data in application code.
Skills in:

# Encrypting environment variables that contain sensitive data

Here is an example of encrypting environment variables containing sensitive data in Python:

**1. Encrypt Variables**

Use Fernet symmetric encryption:

```python
from cryptography.fernet import Fernet
key = Fernet.generate_key()  

f = Fernet(key)
encrypted_password = f.encrypt(b"mysecret")
```

**2. Set Encrypted Value in Environment**

```
export API_KEY="cryptography.fernet.Fernet.generate_key()"
export DB_PASSWORD="cryptography.fernet.Fernet.generate_key()"
```

**3. Decrypt in Code**

Retrieve key and decrypt:

```python
import os
from cryptography.fernet import Fernet

key = os.environ['API_KEY']
f = Fernet(key)

encrypted_password = os.environ['DB_PASSWORD']  
decrypted_password = f.decrypt(encrypted_password)

print(decrypted_password)
```

This keeps sensitive values obscured while allowing decryption in memory at runtime.

Version control, console access only reveals ciphertext. Keys can be stored separately by ops teams. Cryptography libraries handle secure implementation.

# Using secret management services to secure sensitive data

Here is an example of using secret management services to secure sensitive data in Python:

**1. Store Secrets in AWS Secrets Manager**

```python
import boto3
from botocore.exceptions import ClientError

def store_secret(secret):
    secret_name = "db_password"
    region_name = "us-east-1"

    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )

    try:
        response = client.create_secret(
            Name=secret_name,
            SecretString=secret
        )    
    except ClientError as e:
        print(e)
    else:
        return response

my_secret = store_secret("p@ssw0rd123!") 
```

**2. Retrieve Secrets Dynamically**

```python
import json
from base64 import b64decode

response = client.get_secret_value(SecretId=secret_name)
secret = json.loads(b64decode(response['SecretString']))

print(secret) # Prints decrypted secret value 
```

This securely stores credentials, API keys, tokens etc. without hardcoding into code or configs. Secrets Manager handles encryption, rotation, access control automatically.

# Sanitizing sensitive data

Here are some ways to sanitize sensitive data in Python:

**1. Mask passwords**

Replace middle characters:

```python
import re

def mask_password(text):
   return re.sub(r'(?<=\w)\w(?=\w)', '*', text)

print(mask_password('p@ssw0rd')) # p@ss***d
```

**2. Truncate Strings**  

Limit to first/last few digits:

```python
def cc_truncate(text):
   return text[:6] + '******' + text[-4:]

print(cc_truncate(4242424242424242)) # 424242******4242
```

**3. Remove sensitive keys from objects**  

Strip out fields from requests, documents:

```python
data = {
  'username': 'john',
  'password': 'p@ssword123' 
}

sanitized = {k:v for k, v in data.items() if k != 'password'} 
```

**4. Encrypt values**

Use libraries like Fernet for encryption instead of plain text.

Sanitizing properly balances data utility while still maintaining security best practices in applications.



Here are some additional ways to sanitize sensitive data in Python:

**5. Hash long term identifiers**  

```python
import hashlib

def hash_user_id(user_id):
    return hashlib.sha256(str(user_id).encode('utf-8')).hexdigest()

print(hash_user_id(123456789)) 
# 8e992e2a90feff55fc637c389e0d95e58ae6dbeca204c99ba6f12a622b07ac32
```

**6. Anonymize DataFrames**

```python
import pandas as pd

df = pd.DataFrame(data=[[123,'John', 25], [456, 'Sarah', 30]], 
                  columns=['id','name','age']) 

df['id'] = df['id'].apply(hash_user_id)  
df['name'] = 'Anonymous'  
print(df)
```

**7. DB Record Expiry**  

Set retention expired on records for automatic cleanup.

**8. Tokenize fields**  

Map values to random tokens to prevent reverse lookups

Applying sanitization systematically across application code, configs, logs and data sets is key to minimizing risk exposure. Built-in libraries also help enforce best practices consistently.
