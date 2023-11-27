Pipe is the splitter so can split by newlines to create tally

Everything can usually be done in programming language / cli so our interest is everything outside of those

Main themes = debug - monitor, infrastructure changes, artifact creation, security, scaling, 

Timeline = events = architecture diagram

MOST AWS diagrams are User only or Developer only but for each set of stackholder there is a seperate timeline. Each intersects like a railway network

Example - 

[Building an end-to-end Kubernetes-based DevSecOps software factory on AWS | AWS DevOps Blog (amazon.com)](https://aws.amazon.com/blogs/devops/building-an-end-to-end-kubernetes-based-devsecops-software-factory-on-aws/)

The first diagram doesnt show the app user / inside EKS

For now will use cli as the help function is quick to access

All documentation and study material = parameter selection advice

Related triggers? (list of all triggers?) - Trigger lambda list article here - [AWS Lambda Triggers: What Are They? | Dashbird](https://dashbird.io/blog/what-are-aws-lambda-triggers/) 

API Gateway, Cloudformation, Cloudfront, Eventbridge, Cloudwatch Logs, CodeCommit, CodePipeline, Cognito, Config, Connect, Dynamodb, Kinesis, Kinesis Data Firehose, Lex, MQ, S3, SNS, SQS, Step functions and WAF

How can we use all of these in one loop? 

where do the above fit into amplify and elastic beanstalk?

What about ECS and EKS?

Every Skills Line Item leads to code so therefore to make the experimental timeline we need to have all the seperate concepts first and merge them to get the execution order

# Claude Assisted code as basis to build on

***Domain 4: Troubleshooting and Optimization
Task Statement 1: Assist in a root cause analysis.
Skills in:***

# Debugging code to identify defects

Here are some ways to debug code to identify defects in Python:

1. Use `print` statements:

```python
def sum(x, y):
   print(f"Inputs are: {x} {y}")
   result = x + y 
   print(f"Result: {result}") 
   return result
```

Add temporary prints to output key variables and check values.

2. Use built-in Python debugger pdb:

```
import pdb

def divide(x, y):
   pdb.set_trace()
   return x / y

divide(5, 0)
```

Will stop at breakpoint to inspect stack, variables.

3. Use IDE debugger abilities like breakpoint setting, step through execution.

4. Implement automated testing to catch logical errors: 

```python
import unittest
from calc import sum

class TestSum(unittest.TestCase):

    def test_sum(self): 
        self.assertEqual(sum(3, 5), 8)  
```

5. Enable logging to files and cloud to diagnose crashes:

```python
import logging 
logging.basicConfig(filename='app.log', level=logging.ERROR)
```

So in summary, "print debugging", IDE debuggers, automated tests, and logging help systematically catch bugs without relying solely on manual testing and execution tracking.

The key is instrumenting code to validate correctness of logic at key points.

# Interpreting application metrics, logs, and traces

Interpreting application metrics, logs, and traces in code typically involves:

1. **Ingesting/Streaming Data**: Get the monitoring data into your applications in real-time using services like CloudWatch, Kinesis, SQS:

```python
import boto3
cloudwatch = boto3.client('cloudwatch')
streams = []
while True:
   logs = cloudwatch.get_log_events(logGroupName="myApp")  
   streams.append(logs)
```

2. **Parsing/Normalizing**: Standardize the data formats using regexp, JSON parsers etc:

```python
import json 
for log in streams:
   data = json.loads(log)
   timestamp = data['timestamp'] # Parse fields
```

3. **Analysis**: Apply filters, aggregations, statistical analysis to extract insights: 

```python
from collections import defaultdict
metric_data = defaultdict(list) 

for log in streams:
   metric = log['name'] 
   value = log['value']
   metric_data[metric].append(value)

# Calculate avg, percentiles etc  
```

4. **Visualization**: Plot metrics on charts, create alerts and dashboards:

```python
import matplotlib.pyplot as plt

for metric in metric_data:
   plt.plot(metric_data[metric]) 
   plt.title(metric)
   plt.savefig('metric.png')
```

So in summary, leveraging libraries like JSON, regex, statistics, visualization in code unlocks powerful log/metric analysis abilities with flexibility to customize for your app specifics.

# Querying logs to find relevant data

Here are some ways to query logs to find relevant data in code:

1. Use a log aggregation service like CloudWatch Logs Insights and query using SQL:

```sql
SELECT * FROM log_group 
WHERE http_status = 500
LIMIT 100
```

2. Stream logs to Lambda and filter with Python:

```python
import json

def lambda_handler(event, context):
    for record in event['logEvents']:
        log = json.loads(record['message'])  
        if log['http_status'] == 500:
            print(log)
```

3. Load logs into Elasticsearch and search:

```python
from opensearchpy import OpenSearch 

es = OpenSearch()
res = es.search(index="logs", body={"query": {"match": {"message": "error"}}})
print(res['hits']['hits'])
```

4. Parse log file directly and grep patterns: 

```bash
cat application.log | grep "RUNTIME ERROR"
```

The main idea is leveraging services like CloudWatch, Elasticsearch, or languages like Python and SQL to apply filters, queries, and aggregations instead of manual searching.

Automating relevant data extraction from huge log volumes.

# Implementing custom metrics (for example, CloudWatch embedded metric format [EMF])

Here are a few ways to implement custom metrics in code using CloudWatch Embedded Metric Format (EMF):

1. Instrument application code to publish metrics directly:

```python
import cw_emf
emf = cw_emf.emf()

emf.set_metric(name="ProcessedRecords", unit="Count", value=1024)
emf.put_metric_data()
```

2. Generate EMF JSON programmatically and push:

```python
import json

metric_data = {
   "Metrics": [
      {
         "Name": "UserSignups",
         "Unit": "Count",
         "Value": 1.0
      }
   ]
}

emf_json = json.dumps(metric_data)
# Send json to CloudWatch EMF endpoint
```

3. Create custom metrics proxy/decorator:

```python
def emf_metric(name, unit):
   def decorate(func):       
       def wrapper(*args, **kwargs):
           value = func(*args, **kwargs) 
           # EMF put logic
           return value
       return wrapper
   return decorate

@emf_metric(name="Orders", unit="Count")
def get_orders():
   # Function logic
   return len(orders)
```

So in summary, either explicitly formatting EMF JSON, or using libraries/abstractions over it allows publishing custom metrics directly from app code.

This makes instrumenting key business metrics, workflows easy without manual CloudWatch setup.

# Reviewing application health by using dashboards and insights

Here are some ways to review application health in code using dashboards and insights:

1. Use CloudWatch dashboards and generate graphs automatically:

```python
import boto3
cloudwatch = boto3.client('cloudwatch')

resp = cloudwatch.get_metric_statistics(Namespace='MyApp', MetricName='Latency', Period=60, Statistic='Average')
latency_data = resp['Datapoints']

# Plot graphs, create CloudWatch dashboard
import matplotlib.pyplot as plt
plt.plot(latency_data)
plt.title("Application Latency") 
plt.savefig("app_latency.png")

# Upload image to CloudWatch dashboard
cloudwatch.put_metric_dashboard(DashboardName="MyApp Dashboard", DashboardBody=open("app_latency.png", "rb").read())
```

2. Compute aggregates and statistics for anomalies: 

```python
from scipy import stats
latency_data = get_latency_data() # Fetch data

mean = np.mean(latency_data)
std_dev = np.std(latency_data)

# Check thresholds
if latency_data[-1] > mean + 2*std_dev:  
  send_alarm()
```

3. Correlate metrics and logs for insights into issues:

```python
logs = parse_app_logs() 
errors = [log for log in logs if log['level'] == 'ERROR']

get_metric_data('FailureRate') # Compare for trends  
```

The main idea is leveraging data analysis libraries for aggregations, correlations and visualizations to get insights into application health programatically.

# Troubleshooting deployment failures by using service output logs

Here are some tips for troubleshooting deployment failures using service logs:

**1. Enable deployment logs in your services**

For example, in AWS you can enable deployment logs from services like:

- CloudFormation 
- AWS CodeDeploy
- Elastic Beanstalk
- ECS Task Definition 

These will output logs to CloudWatch Logs when deployments run.

**2. Parse deployment log files**

Use a log parsing library to extract key fields like status, timestamps, resources:

```python
for event in deployment_logs:
    print(event["status"], event["resource"], event["time"])
```

**3. Identify failure events** 

Filter logs on failure statuses, errors, exceptions:

```python
fail_events = [e for e in logs if e["status"] == "FAILED"]
```

**4. Compare across deployment log history**

See if the issue started happening recently versus older deployments:

```python
old_logs = fetch_logs("deployments-2021*") 
new_logs = fetch_logs("deployments-2022*")
```

See when and where failures began being introduced.

**5. Cross-reference infrastructure/app logs**

Correlate failures and timing of issues across services: 

```python
app_errors = get_app_errors(time=deploy_failure_time)
```

This structured inspection of machine-generated deployment logs helps reveal issues without needing to manually piece together what happened across environments. Automated parsing brings out key info needed for diagnosing common deployment failures faster.



***Task Statement 2: Instrument code for observability.***

***Skills in:***

# Implementing an effective logging strategy to record application behavior and state

Here are some best practices for implementing an effective logging strategy in code:

1. Log to a central location like CloudWatch Logs or Elasticsearch to aggregate logs:

```python
import logging 
logging.getLogger().addHandler(cloudwatch.CloudWatchLogHandler()) 
logging.error("Payment failed for order xyz")
```

2. Log using different severity levels - info, warn, error critical:

```python
import logging 
logging.critical("App crashed with error!") #critical issues 
logging.error("API rate exceeded limits") 
logging.info("User logged in") #track events
```

3. Create a common log format using JSON for querying:

```python
import json log = { 
        "level": "error", 
        "event": "payment_failed", 
        "orderid": xyz, 
        "time": datetime.now() 
    } 
json_log = json.dumps(log) 
print(json_log)
```

4. Capture metadata like versions, stack traces, configs:

```python
logging.error("Payment error", exc_info=True, stack_info=True)`
```

5. Sensitive data should be masked or hashed in logs:

```python
masked_cc = hide_cc_middle(cc) 
print(f"Invalid CC number: {masked_cc}")
```

This structured, centralized and standardized technique for logging across services improves troubleshooting, analytics and compliance.

# Implementing code that emits custom metrics

Here are some ways to implement code that emits custom metrics:

**1. Use a metrics library**

Python example with `prometheus_client`:

```python
from prometheus_client import start_http_server, Counter

REQUEST_COUNT = Counter('request_count', 'Total Request Count') 

def handle_request():
    REQUEST_COUNT.inc() 
    # ...

start_http_server(8000)
handle_request()
```

**2. Emit metrics to monitoring backends** 

Send custom metrics to tools like StatsD, Graphite, CloudWatch:

```python
import statsd
stats = statsd.StatsClient()  

def auth_user():
    stats.incr('login_count')
    # ...
```

**3. Create metric decorators**

Wrap functions to auto-count invocations:

```python
def metric(metric_name):
    def decorator(func):
        def wrapper(*args, **kwargs):
            send_metric(metric_name)  
            return func(*args, **kwargs)
        return wrapper
    return decorator

@metric('posts_created')
def create_post(post):
   # ... 
```

**4. Standardize metric metadata**

Use labels, tags, consistent naming schemes:

```python
stats.incr('login_count', tags=['region:us-east']) 
```

This makes custom metric instrumentation reusable, portable and consistent across app code.

# Adding annotations for tracing services

Here are some ways to add annotations for distributed tracing in services:

**1. Instrument trace libraries**

For example, OpenTelemetry tracing:

```python
from opentelemetry import trace
tracer = trace.get_tracer("app_tracer")

with tracer.start_as_current_span("db_query"): 
    # ...
    span.set_attribute("db.rows", row_count)
    span.add_event("Query completed", {"query": sql_query})
```

**2. Capture annotations asynchronously** 

Decorate functions or annotate events without modifying method flow:

```python
from opentelemetry.instrumentation import httpx

@httpx.propagate_traces   
async def checkout(request):
   tracer.add_annotation("Payment started")
   # ...
   tracer.add_annotation("Inventory reserved") 
```

**3. Emit tracing data to backends**

Send annotated spans to monitoring systems:

```python
from opentelemetry import trace
from opentelemetry.exporter import jaeger

tracer = trace.get_tracer(__name__)

jaeger_exporter = jaeger.JaegerSpanExporter(
   service_name="checkout_service",
)

# Register the exporter
trace.get_tracer_provider().add_span_processor(
   jaeger.SimpleSpanProcessor(jaeger_exporter)
) 

tracer.start_span("checkout")
# ...
```

Structured application trace data provides deep insights into workflows, failures and performance optimally.

# Implementing notification alerts for specific actions (for example, notifications about quota limits or deployment completions)

Here are some ways to implement notification alerts for specific actions like quota limits or deployments:

**1. Use CloudWatch alarms**

Get notified via SNS, SQS, Lambda when a metric threshold is crossed:

```python
import boto3
cloudwatch = boto3.client('cloudwatch')

alarm = cloudwatch.put_metric_alarm(
    AlarmName='DailyQuotaExceeded',
    MetricName='MaxQuota', 
    ComparisonOperator='GreaterThanThreshold',
    Threshold=100,
    EvaluationPeriods=1, 
    AlarmActions=['SNS topic ARN']
)
```

**2. Check limits programmatically**

Trigger notifications dynamically from code instead of pre-set thresholds:

```python
from botocore.exceptions import ClientError

try: 
    ec2.run_instances(MinCount=1, MaxCount=1)
except ClientError as e:
   if e.response['Error']['Code'] == 'InstanceLimitExceeded':
        notify_instance_limit_exceeded()  
```

**3. Hook into deployment pipelines**

Publish messages to SNS, SQS on deploy status changes:

```python
if deployment.completed:
    publish_message(topic='deployments', message='Application deployed Successfully')
```

**4. Standardize notifications format** 

Use JSON payload with context and actionable info:

```json
{
   "alert": "limit_exceeded",
   "context": { "quota": "DynamoDB Read Capacity" },
   "timestamp": "2023-02-01T12:00:00", 
   "details": {
       "table": "orders",
       "additional info": "can scale table up if needed" 
   }
}
```

This allows reacting to internal app state changes by piping events to external notification channels. Focused and actionable alerts can be created programmatically when needed.

# Implementing tracing by using AWS services and tools

Here are some ways to implement tracing using AWS services:

**1. Instrument AWS SDK**

The AWS SDKs automatically integrate with X-Ray for tracing requests:

```python
import boto3
from aws_xray_sdk.core import xray_recorder

xray_recorder.begin_segment('my_app')

s3 = boto3.client('s3')
s3.list_buckets() # Traced call

xray_recorder.end_segment()
```

**2. Send custom subsegments**  

Allows capturing custom application methods:

```python
from aws_xray_sdk import global_sdk_config

subsegment = xray_recorder.begin_subsegment('my_func')
# Capture metadata or annotations  
subsegment.put_annotation('key', 'value')
subsegment.end_subsegment()
```

**3. Process streaming traces**  

Capture and filter tracing data asynchronously:  

```python
from aws_xray_sdk.streaming import StreamingXRay

stream = StreamingXRay()
for trace in stream:
   if error in trace['message']:
       notify_error(trace)
```

**4. Capture metrics and logs** 

Correlates X-Ray traces with other data:

```python
xray_recorder.put_annotation('auth_latency', str(auth_time_ms))
xray_recorder.put_metadata('debug', str(debug_info))
```

End-to-end request tracing with X-Ray provides insights into application performance, failures and operations.

***Task Statement 3: Optimize applications by using AWS services and features.
Skills in:***

# Profiling application performance

Here are some effective ways to profile application performance in code:

**1. Use context managers to time blocks**

```python
import time

start = time.perf_counter()
with time_block("cpu_heavy_op"):
   # Perform operation
   pass
end = time.perf_counter() 

print(f"Elapsed: {end-start}")
```

**2. Leverage decorators to measure function timings**

```python
from timeit import default_timer 

def timer(func):
    def inner(*args, **kwargs):
        start = default_timer()
        result = func(*args, **kwargs)        
        end = default_timer()
        print(f"Function {func.__name__} Took {end-start}")
        return result
    return inner

@timer
def long_running(n):
   # Complex logic
   return n
```

**3. Profile hotspots and memory with cProfiler**

```python
import cProfile

cProfile.run('long_running(5)')
# Generates stats on memory and cpu usage
```

**4. Visualize flamegraphs with libraries** 

Easily spot bottlenecks.

Profiling instrumentation gives visibility into the performance of Python code in production, helping identify optimization opportunities without needing to use a debugger.

# Determining minimum memory and compute power for an application

Here are some effective strategies in code to determine the minimum memory and compute requirements for an application:

**1. Use load testing**

Gradually increase requests and monitor resource utilization:

```python
import locust

@locust.task
def index(l):
    l.client.get("/")

locust -u 50 # simulated users    
```

**2. Size workflows**  

Profile representative workflows end-to-end:

```python
@timer
def process_order():
   # Place order logic  
   pass

min_memory = get_memory_usage() 
```

**3. Set lower bounds in config**

```python
min_instances = 1
min_memory = 512MB # MB
min_cpu = 0.5 # vCPUs

config = {
  "instaces": max(num_instances, min_instances),
  "memory": max(total_memory, min_memory),
  "cpu": max(total_vcpu, min_cpu)
}
```

**4. Over-provision in staging** 

Test with excess capacity and scale down to save costs.

Automated sizing eliminates guess-work. Optimally right-sized apps save resources without sacrificing performance.

# Using subscription filter policies to optimize messaging

Here are some ways to use subscription filter policies to optimize messaging workflows:

**1. Reduce unwanted messages**

```
{
   "region": ["us-east-1"],
   "eventType": ["order_created"]    
}
```

**2. Split event streams** 

Route types to different consumers:

```
{
   "userType": ["premium"]
}
```

```
{
   "userType": ["basic"]  
} 
```

**3. Fan-out locality based**

```
{
  "country": ["United States"] 
}
```

```
{
   "country": ["Canada"]
} 
```

**4. Implement with SNS/SQS**

```python
import json
from boto3 import client

sns = client("sns") 
queue = client("sqs")

filter_policy = {
  "region": ["us-east-1"]
}  

queue_arn = queue.create_queue(Attributes={"FilterPolicy":json.dumps(filter_policy)})
topic.subscribe(queue_arn)
```

Fine-grained stream filtering reduces unnecessary data transfer and computation downstream optimizing for cost, throughput, and latency.

# Caching content based on request headers

Here are some examples of caching content based on request headers in code:

**1. Check User-Agent header** 

```python
from flask import request

@app.route('/data')
def data():
    user_agent = request.headers.get('User-Agent')
    if user_agent == MOBILE_USER_AGENT:
        return cache.get('mobile_data')
    else:
        return cache.get('standard_data')
```

**2. Vary cache by Accept-Language**

```python
lang = request.headers.get('Accept-Language')
if lang.startswith('es'):
    return cache.get('es_data')
else: 
    return cache.get('en_data')
```

**3. Custom header-based versioning**

```python
version = request.headers.get('Api-Version')
key = f'data:v{version}'
return cache.get(key) 
```

**4. Hash header values**  

```python
etag = hash(request.headers) 
key = f'data:{etag}'
return cache.get(key)
```

This allows caching multiple representations optimized for different consumers like devices, locales, API versions etc., reducing duplicate generation and transfer of data.
