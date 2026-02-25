<!-- ===================================================== -->
<!--                AWS CloudFront Documentation           -->
<!--     Professional-Level Guide with Public Images      -->
<!-- ===================================================== -->

<h1 align="center" style="color:#ff9900;">
🌍 AWS CloudFront
</h1>

<p align="center">
<b>Global CDN • Low Latency • Secure • Highly Scalable</b><br>
Content Delivery Network (CDN) by Amazon Web Services
</p>

<hr>

<h2>🧠 What is AWS CloudFront?</h2>

<p>
<b>AWS CloudFront</b> is a global Content Delivery Network (CDN) that securely delivers
web content, APIs, videos, and applications with low latency and high transfer speeds.
</p>

<p>
Instead of serving content from one central server, CloudFront distributes copies
of your content across global <b>edge locations</b>.
</p>

<img src="https://docs.aws.amazon.com/images/AmazonCloudFront/latest/DeveloperGuide/images/how-you-configure-cf.png" width="100%">

<p align="center">
CloudFront delivers content from the nearest edge location to the user.
</p>

<hr>

<h2>🌎 Why CloudFront is Important</h2>

<h3>Without CloudFront</h3>

<pre>
User (Germany) → Server (US-East-1) → High latency
</pre>

<h3>With CloudFront</h3>

<pre>
User (Germany) → Frankfurt Edge Location → Low latency
</pre>

<p>
This dramatically reduces:
</p>
<ul>
<li>Latency</li>
<li>Server load</li>
<li>Bandwidth cost</li>
<li>Time to first byte (TTFB)</li>
</ul>

<hr>

<h2>🏗 CloudFront Architecture</h2>


<pre>
User Request
     ↓
CloudFront Edge Location
     ↓ (Cache Hit)
Return Cached Content

OR (Cache Miss)
     ↓
Origin (S3 / ALB / EC2 / API Gateway)
     ↓
Cache at Edge
     ↓
Return to User
</pre>

<hr>

<h2>🔑 Core Components</h2>

<h3>1️⃣ Distribution</h3>
<p>
Main configuration unit of CloudFront.
Defines:
</p>
<ul>
<li>Origin</li>
<li>Caching rules</li>
<li>Security policies</li>
<li>Behaviors</li>
</ul>

<hr>

<h3>2️⃣ Edge Locations</h3>
<p>
AWS global data centers where content is cached.
</p>

<p>
CloudFront has hundreds of edge locations worldwide.
</p>

<hr>

<h3>3️⃣ Origin</h3>

<p>
The source of content. Examples:
</p>

<ul>
<li>Amazon S3</li>
<li>Application Load Balancer</li>
<li>EC2 Instance</li>
<li>API Gateway</li>
</ul>

<hr>

<h2>⚡ How Caching Works</h2>

<h3>Cache Hit</h3>
<pre>
User → Edge → Served instantly
</pre>

<h3>Cache Miss</h3>
<pre>
User → Edge → Origin → Cache → User
</pre>

<hr>

<h2>⏱ TTL (Time to Live)</h2>

<p>
TTL controls how long content stays cached at edge locations.
</p>

<ul>
<li>Minimum TTL</li>
<li>Default TTL</li>
<li>Maximum TTL</li>
</ul>

<hr>

<h2>🔐 Security Features</h2>

<ul>
<li>HTTPS (SSL/TLS)</li>
<li>Custom domain with ACM</li>
<li>Signed URLs / Cookies</li>
<li>Origin Access Control (OAC)</li>
<li>AWS WAF integration</li>
<li>DDoS protection with AWS Shield</li>
</ul>


<hr>

<h2>🚀 Example 1: Static Website (S3 + CloudFront)</h2>



<pre>
User
  ↓
CloudFront
  ↓
Private S3 Bucket
</pre>

Benefits:
<ul>
<li>Global caching</li>
<li>HTTPS enabled</li>
<li>S3 not publicly exposed</li>
<li>Better security</li>
</ul>

<hr>

<h2>🚀 Example 2: API Acceleration</h2>


<pre>
User
  ↓
CloudFront
  ↓
Application Load Balancer
  ↓
ECS / EC2 Backend
</pre>

<hr>

<h2>🔄 Detailed Request Flow</h2>

<pre>
1. User sends HTTPS request
2. DNS resolves to CloudFront
3. Nearest edge location receives request
4. Edge checks cache
5. If miss → forward to origin
6. Origin responds
7. Edge caches response
8. Response returned to user
</pre>

<hr>

<h2>💰 Pricing Overview</h2>

CloudFront pricing depends on:
<ul>
<li>Data transfer out (GB)</li>
<li>HTTP/HTTPS requests</li>
<li>Invalidation requests</li>
</ul>

Cost optimization:
<ul>
<li>Use correct TTL values</li>
<li>Compress static content</li>
<li>Version files to avoid invalidations</li>
</ul>

<hr>

<h2>🧩 Advanced Features</h2>

<ul>
<li>Lambda@Edge (run code at edge)</li>
<li>CloudFront Functions</li>
<li>Geo restriction</li>
<li>Field-level encryption</li>
<li>Multi-origin failover</li>
</ul>

<hr>

<h2>📌 Real-World Production Pattern</h2>

<pre>
CloudFront
   ↓
ALB
   ↓
ECS Fargate
   ↓
RDS
</pre>

<p>
CloudFront acts as:
</p>
<ul>
<li>Global entry point</li>
<li>Security shield</li>
<li>Performance accelerator</li>
<li>DDoS protection layer</li>
</ul>

<hr>

<h2>🎯 Best Practices</h2>

<ul>
<li>Always enable HTTPS</li>
<li>Keep S3 bucket private</li>
<li>Use Origin Access Control</li>
<li>Separate static & dynamic behaviors</li>
<li>Enable logging</li>
<li>Use versioned file names</li>
</ul>

<hr>

<h2 align="center">🌎 CloudFront = Performance + Security + Global Scale</h2>