My programming choices for now are cli for once off, python for everything else and terraform for infrastructure

# (Claude assisted commands)

# Billing State - cli - per service (adjust the date)

aws ce get-cost-and-usage --time-period Start=2023-11-01,End=2023-11-27 --granularity MONTHLY --metric BLENDED_COST --group-by Type=DIMENSION,Key=SERVICE

# Billing State - Lambda - same as above but python and one week length

import boto3 

from datetime import datetime, timedelta 

ce = boto3.client('ce') 

start_date = datetime.now() - timedelta(days=7) 

end_date = datetime.now() 

start_date_str = start_date.strftime("%Y-%m-%d") 

end_date_str = end_date.strftime("%Y-%m-%d") 

response = ce.get_cost_and_usage( TimePeriod={ 'Start': start_date_str, 'End': end_date_str }, Granularity='MONTHLY', Metrics=['BLENDED_COST'], GroupBy=[ { 'Type': 'DIMENSION', 'Key': 'SERVICE' }, ] ) 

print(response)

# List All resources

aws resourcegroupstaggingapi get-resources  

/and                > CurrentAWSResources.txt



`aws resourcegroupstaggingapi get-resources --query 'ResourceTagMappingList[*].ResourceARN' --output json | jq` pipe to jq?

# Add Existing resources to Terraform

terraform import aws_instance.my_ec2 i-number

`terraform state list` or terraform state show

terraform refresh
