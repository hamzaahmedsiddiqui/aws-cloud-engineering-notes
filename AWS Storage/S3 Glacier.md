<h2 style="color:#ff9900;">Amazon S3 Glacier</h2>
Amazon S3 Glacier is a storage service purpose-built for data archiving. It provides high performance, flexible retrieval, and low-cost archive storage in the cloud.

<h3 style="color:#ff9900;">Amazon S3 Glacier storage classes </h3>

![Alt](/images/s3-glacier-classes.png)
1. **S3 Glacier Instant Retrieval**: This storage class is designed for data that requires immediate access. It offers millisecond retrieval times, making it ideal for active archives and data that needs to be accessed frequently.
2. **S3 Glacier Flexible Retrieval**: This storage class is suitable for data that can
tolerate retrieval times of minutes to hours. It provides a cost-effective solution for long-term data archiving and backup.
3. **S3 Glacier Deep Archive**: This storage class is designed
for data that is rarely accessed and can tolerate retrieval times of up to 12 hours. It offers the lowest cost storage option for long-term data archiving and backup.

Data volumeNo limitNo limitAverage latencyMillisecondsMinutes or hoursItem size5 TB max40 TB maxCost per GB per month¢ ¢¢Billed requestsPUT, COPY, POST, LIST, and GETUPLOAD and retrievalRetrieval pricing¢¢ ¢

<h3 style="color:#ff9900;">Comparing Amazon S3 and Amazon S3 Glacier in table </h3>

| Feature | Amazon S3 | Amazon S3 Glacier |
| --- | --- | --- |
| Storage Class | Standard, Intelligent-Tiering, One Zone-IA, Glacier Instant Retrieval,
Glacier Flexible Retrieval, Glacier Deep Archive | Glacier Instant Retrieval, Glacier Flexible Retrieval, Glacier Deep Archive |
| Use Cases | Frequently accessed data, data with unknown access patterns, data that requires high durability
| Data archiving, long-term backup, data that can tolerate longer retrieval times |
| Retrieval Time | Milliseconds to seconds | Minutes to hours |
| Cost | Higher cost for frequently accessed data | Lower cost for infrequently accessed data |
| Data Volume | No limit | No limit |
| Item Size | 5 TB max | 40 TB max |


<h3 style="color:#ff9900;">Security comparison</h3>

| Feature | Amazon S3 | Amazon S3 Glacier |
| --- | --- | --- |
| Encryption | Server-side encryption (SSE-S3, SSE-KMS, SSE-C),
Client-side encryption | Server-side encryption (SSE-S3, SSE-KMS, SSE-C), Client-side encryption |
| Access Control | IAM policies, Bucket policies, ACLs | IAM policies, Vault access policies |
| Data Integrity | MD5 checksums, Versioning | MD5 checksums, Versioning
### 
<h3 style="color:#ff9900;">Conclusion</h3>

Amazon S3 and Amazon S3 Glacier are both powerful storage services offered by AWS, but they
are designed for different use cases. Amazon S3 is ideal for frequently accessed data and offers a variety of storage classes to meet different needs, while Amazon S3 Glacier is optimized for long-term data archiving and backup with lower costs for infrequently accessed data. When choosing between the two, consider your specific requirements for access patterns, retrieval times, and cost to determine which service best fits your needs.



