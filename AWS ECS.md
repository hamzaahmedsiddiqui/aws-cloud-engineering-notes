<!-- ===================================================== -->
<!--          Amazon ECS (Elastic Container Service)      -->
<!--        Single Markdown File using HTML only          -->
<!-- ===================================================== -->

<h1 align="center">🚢 Amazon ECS (Elastic Container Service)</h1>

<p align="center">
<b>Run Docker containers on AWS without managing everything manually.</b><br>
Fully managed • Scalable • Integrated with VPC • Production-ready
</p>

<hr>

<h2>🧠 What is Amazon ECS?</h2>

<p>
<b>Amazon ECS</b> is AWS’s container orchestration service.
It allows you to run, scale, and manage Docker containers in the cloud.
</p>

<p>
You provide:
<ul>
<li>Docker image</li>
<li>CPU & memory requirements</li>
<li>Networking configuration</li>
</ul>

AWS provides:
<ul>
<li>Scheduling</li>
<li>Scaling</li>
<li>Health monitoring</li>
<li>Infrastructure (if using Fargate)</li>
</ul>
</p>

<hr>

<h2>📊 High-Level Architecture</h2>

<img src="https://docs.aws.amazon.com/images/AmazonECS/latest/developerguide/images/ecs-architecture-overview.png" width="100%">

<p align="center">
ECR → Task Definition → Service → Cluster → (EC2 or Fargate)
</p>

<hr>

<h2>🏗 Core Components Explained</h2>

<h3>1️⃣ Cluster</h3>
<p>
A cluster is a logical grouping of compute capacity.
It is where your containers run.
</p>

<ul>
<li>Can use EC2 instances</li>
<li>Or Fargate (serverless compute)</li>
</ul>

<hr>

<h3>2️⃣ Task Definition</h3>

<p>
A Task Definition is a blueprint describing how to run your container.
</p>

Includes:
<ul>
<li>Docker image</li>
<li>CPU & memory</li>
<li>Port mappings</li>
<li>Environment variables</li>
<li>IAM roles</li>
<li>Logging configuration</li>
</ul>

<pre>
{
  "family": "my-api",
  "cpu": "256",
  "memory": "512",
  "containerDefinitions": [
    {
      "name": "app",
      "image": "123456789012.dkr.ecr.us-west-2.amazonaws.com/my-api:latest",
      "portMappings": [
        { "containerPort": 3000 }
      ]
    }
  ]
}
</pre>

<hr>

<h3>3️⃣ Task</h3>

<p>
A Task is a running instance of a Task Definition.
</p>

<p>
Blueprint = Task Definition<br>
Running container = Task
</p>

<hr>

<h3>4️⃣ Service</h3>

<p>
A Service ensures:
</p>

<ul>
<li>Desired number of tasks stay running</li>
<li>Automatic restarts on failure</li>
<li>Load balancer integration</li>
<li>Auto scaling</li>
</ul>

<p>
Without a Service → container crashes and stays down.<br>
With a Service → ECS replaces it automatically.
</p>

<hr>

<h2>🚀 Launch Types</h2>

<h3>☁️ Fargate (Serverless)</h3>

<ul>
<li>No EC2 management</li>
<li>You define CPU & memory</li>
<li>AWS manages infrastructure</li>
<li>Best for startups and microservices</li>
</ul>

<hr>

<h3>🖥 EC2 Launch Type</h3>

<ul>
<li>You manage EC2 instances</li>
<li>More control</li>
<li>Often cheaper at scale</li>
<li>Requires patching & scaling management</li>
</ul>

<hr>

<h2>⚖️ EC2 vs Fargate</h2>

<table border="1" cellpadding="8">
<tr>
<th>Feature</th>
<th>Fargate</th>
<th>EC2</th>
</tr>
<tr>
<td>Server Management</td>
<td>AWS</td>
<td>You</td>
</tr>
<tr>
<td>Ease of Setup</td>
<td>Very Easy</td>
<td>Medium</td>
</tr>
<tr>
<td>Cost at Scale</td>
<td>Higher</td>
<td>Lower</td>
</tr>
<tr>
<td>Flexibility</td>
<td>Good</td>
<td>High</td>
</tr>
</table>

<hr>

<h2>🌐 Networking in ECS</h2>

<p>
ECS runs inside your VPC.
</p>

Typical production architecture:
</p>

<img src="https://docs.aws.amazon.com/images/AmazonECS/latest/developerguide/images/alb-service.png" width="100%">

<ul>
<li>ALB in Public Subnet</li>
<li>ECS Tasks in Private Subnet</li>
<li>RDS in Private Subnet</li>
<li>NAT Gateway for outbound internet</li>
</ul>

<hr>

<h2>🔐 IAM Roles in ECS</h2>

<h3>1️⃣ Task Execution Role</h3>
<ul>
<li>Pull image from ECR</li>
<li>Send logs to CloudWatch</li>
<li>Access Secrets Manager</li>
</ul>

<h3>2️⃣ Task Role</h3>
<ul>
<li>Used by your app inside container</li>
<li>Access S3, DynamoDB, SQS, etc.</li>
</ul>

<p><b>Never hardcode AWS credentials in containers.</b></p>

<hr>

<h2>📈 Auto Scaling</h2>

ECS can scale based on:

<ul>
<li>CPU usage</li>
<li>Memory usage</li>
<li>Custom CloudWatch metrics</li>
</ul>

Example logic:

<pre>
If CPU > 70% → Increase tasks
If CPU < 30% → Decrease tasks
</pre>

<hr>

<h2>⚖️ Load Balancers</h2>

<h3>Application Load Balancer (ALB)</h3>
<ul>
<li>HTTP/HTTPS routing</li>
<li>SSL termination</li>
<li>Path-based routing</li>
<li>Health checks</li>
</ul>

<h3>Network Load Balancer (NLB)</h3>
<ul>
<li>Layer 4 (TCP/UDP)</li>
<li>High performance</li>
</ul>

<hr>

<h2>📡 Logging & Monitoring</h2>

<ul>
<li>CloudWatch Logs</li>
<li>CloudWatch Metrics</li>
<li>AWS X-Ray</li>
<li>CloudTrail</li>
</ul>

<hr>

<h2>🔁 Deployment Flow</h2>

<pre>
1. Build Docker Image
2. Push to Amazon ECR
3. Update ECS Task Definition
4. Deploy ECS Service
5. Rolling update begins
</pre>

Modern CI/CD flow:

<pre>
Git Push
   ↓
CI Pipeline
   ↓
Docker Build
   ↓
Push to ECR
   ↓
Deploy to ECS
</pre>

<hr>

<h2>🆚 ECS vs EKS</h2>

<table border="1" cellpadding="8">
<tr>
<th></th>
<th>ECS</th>
<th>EKS</th>
</tr>
<tr>
<td>Complexity</td>
<td>Lower</td>
<td>Higher</td>
</tr>
<tr>
<td>Uses Kubernetes</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>Best For</td>
<td>AWS-native apps</td>
<td>Kubernetes ecosystem</td>
</tr>
</table>

<hr>

<h2>🎯 When Should You Use ECS?</h2>

<ul>
<li>Running Docker containers</li>
<li>Building scalable APIs</li>
<li>Microservices architecture</li>
<li>Want AWS-native solution</li>
<li>Need production-ready container orchestration</li>
</ul>

<hr>

<h2>🧩 Final Mental Model</h2>

<pre>
ECR → Stores Images
Task Definition → Blueprint
Task → Running Container
Service → Keeps Tasks Alive
Cluster → Infrastructure
Launch Type → EC2 or Fargate
</pre>

<hr>

<h3 align="center">🚀 ECS is the production-grade way to run containers on AWS.</h3>