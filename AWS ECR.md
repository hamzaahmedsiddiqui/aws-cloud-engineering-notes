<!-- ===================================================== -->
<!--        Amazon Elastic Container Registry (ECR)       -->
<!--                Clean HTML Documentation               -->
<!-- ===================================================== -->

<h1 align="center" style="color:#ff9900;">
📦 Amazon Elastic Container Registry (Amazon ECR)
</h1>

<p align="center">
<b>Secure • Fully Managed • Scalable Docker Image Registry on AWS</b>
</p>

<hr>

<h2>🧠 What is Amazon ECR?</h2>

<p>
<b>Amazon Elastic Container Registry (ECR)</b> is a fully managed container image registry service provided by AWS.
It allows you to securely store, manage, version, and deploy Docker container images at scale.
</p>

<p>
In simple terms:
</p>

<pre>
You build Docker image → Push to ECR → Deploy to ECS / EKS / Lambda
</pre>

<p>
ECR acts like a private Docker Hub, but deeply integrated into the AWS ecosystem.
</p>

<hr>

<h2>🏗 Why Amazon ECR Exists</h2>

<p>
When working with containers, you need a central place to store images.
That place must be:
</p>

<ul>
<li>Secure</li>
<li>Highly available</li>
<li>Scalable</li>
<li>Integrated with deployment services</li>
</ul>

<p>
Amazon ECR solves this by providing a production-grade registry managed entirely by AWS.
</p>

<hr>

<h2>✨ Key Features of Amazon ECR</h2>

<h3>1️⃣ Fully Managed</h3>
<p>
You do not manage:
</p>
<ul>
<li>Servers</li>
<li>Scaling</li>
<li>Replication</li>
<li>Availability</li>
</ul>

<p>
AWS handles infrastructure, patching, scaling, and durability.
You focus on building and shipping your application.
</p>

<hr>

<h3>2️⃣ Enterprise-Grade Security</h3>

<ul>
<li>Encryption at rest (AWS-managed encryption)</li>
<li>Encryption in transit (HTTPS)</li>
<li>IAM-based access control</li>
<li>Private repositories</li>
<li>Image scanning for vulnerabilities</li>
</ul>

<p>
Access is controlled using <b>AWS IAM policies</b>, meaning you can define exactly:
</p>

<ul>
<li>Who can push images</li>
<li>Who can pull images</li>
<li>Who can delete images</li>
</ul>

<hr>

<h3>3️⃣ High Scalability & Availability</h3>

<p>
Amazon ECR automatically scales to handle:
</p>

<ul>
<li>Thousands of image pulls</li>
<li>Large repositories</li>
<li>High traffic production workloads</li>
</ul>

<p>
It is regionally available and highly durable.
</p>

<hr>

<h3>4️⃣ Deep Integration with AWS Services</h3>

<p>
ECR integrates seamlessly with:
</p>

<ul>
<li><b>Amazon ECS</b></li>
<li><b>Amazon EKS</b></li>
<li><b>AWS Lambda</b> (container-based functions)</li>
<li><b>AWS CodeBuild / CodePipeline</b></li>
<li><b>IAM</b></li>
</ul>

<p>
No additional configuration is required — AWS services authenticate automatically using IAM roles.
</p>

<hr>

<h3>5️⃣ Vulnerability Scanning</h3>

<p>
Amazon ECR can scan images for known vulnerabilities using AWS security databases.
</p>

<p>
This helps you:
</p>

<ul>
<li>Detect insecure dependencies</li>
<li>Improve DevSecOps practices</li>
<li>Maintain production-grade security posture</li>
</ul>

<hr>

<h2>📦 Key Concepts in Amazon ECR</h2>

<h3>🔹 Repository</h3>
<p>
A repository is a collection of related container images.
</p>

Example:
</p>

<pre>
my-backend-repo
my-frontend-repo
payment-service-repo
</pre>

<p>
Each repository stores multiple versions (tags) of images.
</p>

<hr>

<h3>🔹 Image</h3>

<p>
An image is the packaged version of your application including:
</p>

<ul>
<li>Application code</li>
<li>Dependencies</li>
<li>Runtime</li>
<li>Configuration</li>
</ul>

Example image tag:
</p>

<pre>
my-api:1.0.0
my-api:latest
</pre>

<hr>

<h3>🔹 Image Tags</h3>

<p>
Tags help you version images.
</p>

Best practice:
</p>

<ul>
<li>Avoid using only <code>latest</code> in production</li>
<li>Use semantic versioning (1.0.0, 1.0.1, etc.)</li>
</ul>

<hr>

<h3>🔹 Lifecycle Policies</h3>

<p>
Lifecycle policies automatically delete old or unused images.
</p>

Example:
</p>

<ul>
<li>Keep last 10 images</li>
<li>Delete images older than 30 days</li>
</ul>

<p>
This helps control storage costs.
</p>

<hr>

<h2>💰 Pricing Model</h2>

<ul>
<li>Pay only for image storage (per GB per month)</li>
<li>Pay for outbound data transfer</li>
<li>Free tier available for new AWS accounts</li>
<li>Public repositories have different pricing rules</li>
</ul>

<p>
No cost for pushing images within the same AWS region.
</p>

<hr>

<h2>🔄 Typical Workflow with Amazon ECR</h2>

<pre>
1. Build Docker Image
2. Authenticate to ECR
3. Tag the image
4. Push image to ECR
5. Deploy image via ECS/EKS/Lambda
</pre>

Example commands:

<pre>
aws ecr get-login-password --region us-west-2 | \
docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-west-2.amazonaws.com

docker build -t my-api .
docker tag my-api:latest 123456789012.dkr.ecr.us-west-2.amazonaws.com/my-api:1.0.0
docker push 123456789012.dkr.ecr.us-west-2.amazonaws.com/my-api:1.0.0
</pre>

<hr>

<h2>🚀 Common Use Cases</h2>

<ul>
<li>Storing Docker images for ECS or EKS workloads</li>
<li>CI/CD pipelines pushing images automatically</li>
<li>Serverless container deployments using Lambda</li>
<li>Multi-environment image versioning (dev, staging, prod)</li>
<li>Secure enterprise container registry</li>
</ul>

<hr>

<h2>🛡 Best Practices</h2>

<ul>
<li>Use IAM roles instead of access keys</li>
<li>Enable image scanning</li>
<li>Use lifecycle policies</li>
<li>Use immutable tags in production</li>
<li>Limit repository access with least privilege</li>
</ul>

<hr>

<h2>🧩 How ECR Fits in Modern Cloud Architecture</h2>

<pre>
Developer → Git Push
       ↓
CI/CD Pipeline
       ↓
Docker Build
       ↓
Push to ECR
       ↓
Deploy to ECS/EKS
       ↓
Production
</pre>

<p>
ECR acts as the central container image hub in your DevOps workflow.
</p>

<hr>

<h2>🎯 Conclusion</h2>

<p>
Amazon Elastic Container Registry (ECR) is a secure, scalable, and fully managed container registry designed for modern cloud-native applications.
</p>

<p>
It eliminates the operational burden of managing your own Docker registry while integrating tightly with AWS services.
</p>

<p>
If you are building containerized applications on AWS,
<b>Amazon ECR is the foundation for managing your container images safely and efficiently.</b>
</p>

<hr>

<p align="center">
🚀 Secure your containers. Scale with confidence. Deploy with simplicity.
</p>