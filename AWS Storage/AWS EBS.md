<!-- =========================
     Amazon EBS (SAA-C03 level)
     ========================= -->

<section style="font-family: Arial, sans-serif; line-height: 1.55; max-width: 980px; margin: 0 auto;">

  <h1 style="color:#ff9900; margin-bottom: 6px;">Amazon Elastic Block Store (Amazon EBS)</h1>
  <p style="margin-top: 0; color:#333;">
    <b>Amazon EBS</b> is AWS’s <b>persistent block storage</b> designed primarily for <b>Amazon EC2</b>. 
    You can think of an EBS volume as a <b>virtual hard drive</b> that you attach to an instance. 
    It’s built for <b>low-latency</b>, predictable performance, and data durability — which is why it’s commonly used for 
    databases, boot volumes, and workloads that need consistent I/O.
  </p>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 16px; border-radius:10px; margin: 14px 0;">
    <h3 style="margin:0 0 8px; color:#ff9900;">Exam mindset (Solution Architect)</h3>
    <ul style="margin:0; padding-left: 18px;">
      <li><b>EBS is AZ-scoped</b> (a volume lives in <b>one</b> Availability Zone).</li>
      <li><b>Snapshots live in S3</b> (managed by AWS) and are used for backup/restore and copying across Regions.</li>
      <li><b>Multi-AZ replication</b> is a feature of services like <b>RDS Multi-AZ</b>, not “EBS volumes replicate across multiple AZs.”</li>
      <li><b>Performance</b> depends on volume type + size + IOPS/throughput settings and (for some types) instance support.</li>
    </ul>
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin: 18px 0;"/>

  <h2 style="color:#ff9900;">What “block storage” means</h2>
  <p style="color:#333;">
    Block storage stores data in fixed-size blocks and exposes it like a disk device to the OS.
    That’s different from:
  </p>
  <ul style="color:#333;">
    <li><b>Object storage</b> (Amazon S3): great for files, backups, static content, analytics.</li>
    <li><b>File storage</b> (Amazon EFS): shared POSIX file system across many instances.</li>
  </ul>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 16px; border-radius:10px; margin: 14px 0;">
    <b>Quick rule:</b> If you need a disk for an EC2 instance → EBS.  
    If you need shared Linux file storage → EFS.  
    If you need durable object storage / static hosting / backup repository → S3.
  </div>

  <h2 style="color:#ff9900;">Core features (what matters most)</h2>
  <ul style="color:#333;">
    <li><b>Persistent storage</b>: Data remains even if the EC2 instance stops/starts (as long as you don’t delete the volume).</li>
    <li><b>AZ-level durability</b>: EBS is designed to be resilient within an Availability Zone. (The volume is not a multi-AZ resource.)</li>
    <li><b>Encryption</b>: Supports encryption at rest (KMS), and encryption is simple to enable for new volumes (and possible via snapshots for existing ones).</li>
    <li><b>Elastic volumes</b>: You can often modify volume type, size, and performance settings with minimal disruption (OS may still need resizing).</li>
    <li><b>Snapshots</b>: Point-in-time backups stored in S3, incremental after the first snapshot.</li>
    <li><b>Integration</b>: Works tightly with EC2, Auto Scaling, AMIs, backup workflows, and DR patterns.</li>
  </ul>

  <h2 style="color:#ff9900;">EBS volume types (SAA-level summary)</h2>
  <p style="color:#333;">
    Choose volume types based on workload characteristics: random I/O vs sequential throughput, latency sensitivity, and cost.
  </p>

  <table style="border-collapse: collapse; width:100%; font-size: 14px;">
    <thead>
      <tr style="background:#fff3e0;">
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Type</th>
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Best for</th>
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Key exam notes</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><b>gp3</b> (General Purpose SSD)</td>
        <td style="border:1px solid #eee; padding:10px;">Default for most workloads</td>
        <td style="border:1px solid #eee; padding:10px;">Cost-effective, lets you scale IOPS/throughput separately from size</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><b>io1/io2</b> (Provisioned IOPS SSD)</td>
        <td style="border:1px solid #eee; padding:10px;">High IOPS, latency-sensitive DB workloads</td>
        <td style="border:1px solid #eee; padding:10px;">Pick when you need guaranteed IOPS (enterprise DB, heavy OLTP)</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><b>st1</b> (Throughput Optimized HDD)</td>
        <td style="border:1px solid #eee; padding:10px;">Big sequential workloads</td>
        <td style="border:1px solid #eee; padding:10px;">Good for log processing, data warehouses (not boot)</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><b>sc1</b> (Cold HDD)</td>
        <td style="border:1px solid #eee; padding:10px;">Infrequently accessed, large data</td>
        <td style="border:1px solid #eee; padding:10px;">Lowest cost HDD (not boot), slower</td>
      </tr>
    </tbody>
  </table>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 16px; border-radius:10px; margin: 14px 0;">
    <b>Important correction:</b> Your original text mentioned “gp2” and “io1” as examples.  
    For modern exam prep, you should know <b>gp3</b> and <b>io2</b> are commonly referenced along with gp2/io1.
  </div>

  <h2 style="color:#ff9900;">Snapshots, AMIs, and restore flow</h2>
  <p style="color:#333;">
    Snapshots are the backbone of backup and disaster recovery for EC2 storage.
  </p>

  <ol style="color:#333;">
    <li><b>Create snapshot</b> of an EBS volume (stored in S3; incremental after first snapshot).</li>
    <li><b>Copy snapshot</b> to another Region (for regional DR).</li>
    <li><b>Create a new volume</b> from the snapshot in the target AZ/Region.</li>
    <li><b>Attach</b> that volume to an EC2 instance and mount it.</li>
  </ol>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 16px; border-radius:10px; margin: 14px 0;">
    <b>AMIs:</b> An AMI for EBS-backed instances typically uses EBS snapshots underneath.  
    In exams, AMIs are often the “golden image” approach for fast recovery and consistent provisioning.
  </div>

  <h2 style="color:#ff9900;">Availability, resilience, and DR (what to say correctly)</h2>
  <ul style="color:#333;">
    <li><b>EBS volumes are AZ-specific</b>. If an AZ is down, that volume is unavailable.</li>
    <li>To survive AZ failure, you typically design at the <b>application layer</b>:
      <ul>
        <li>Run instances in multiple AZs (Auto Scaling group across AZs).</li>
        <li>Use <b>load balancing</b> (ALB/NLB) across AZs.</li>
        <li>Use data-layer approaches like <b>RDS Multi-AZ</b>, <b>replication</b>, or <b>restore from snapshot</b>.</li>
      </ul>
    </li>
    <li>For <b>Region-level DR</b>, copy snapshots cross-Region, and use Route 53 failover / active-active patterns.</li>
  </ul>

  <h2 style="color:#ff9900;">Performance and limits (exam-friendly)</h2>
  <ul style="color:#333;">
    <li><b>IOPS</b> = number of reads/writes per second (random I/O heavy workloads care a lot).</li>
    <li><b>Throughput</b> = MB/s (large sequential read/write workloads care a lot).</li>
    <li>Instance type matters (some instances can drive higher EBS bandwidth/IOPS).</li>
    <li><b>RAID</b> can be used to combine volumes for performance or redundancy (architectural choice, not a “default EBS feature”).</li>
  </ul>

  <h2 style="color:#ff9900;">Common use cases</h2>
  <ul style="color:#333;">
    <li><b>Boot volumes</b> for EC2 instances.</li>
    <li><b>Databases</b> on EC2 (especially with io1/io2 for consistent performance).</li>
    <li><b>Application data</b> that needs fast reads/writes and durability.</li>
    <li><b>Backup & restore</b> using snapshots (including cross-Region copies for DR).</li>
    <li><b>Lift-and-shift</b> workloads that expect a traditional disk attached to a server.</li>
  </ul>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 16px; border-radius:10px; margin: 14px 0;">
    <h3 style="margin:0 0 8px; color:#ff9900;">Mistakes to avoid in exam answers</h3>
    <ul style="margin:0; padding-left: 18px;">
      <li>Saying “EBS replicates across multiple AZs.” (It doesn’t. It’s <b>single-AZ</b>.)</li>
      <li>Choosing EBS for shared file storage across many instances (that’s usually <b>EFS</b>).</li>
      <li>Choosing HDD types for latency-sensitive databases (SSD types are usually the answer).</li>
      <li>Assuming “resize without downtime” always means zero operational steps (OS/filesystem resizing may be needed).</li>
    </ul>
  </div>

  <h2 style="color:#ff9900;">Conclusion</h2>
  <p style="color:#333;">
    Amazon EBS is the go-to service for <b>persistent, low-latency block storage</b> attached to EC2. 
    For Solution Architect prep, the big concepts are: <b>AZ scope</b>, volume type selection (<b>gp3</b> vs <b>io2</b> vs HDD),
    and how <b>snapshots</b> enable backup, migration, and disaster recovery. 
    If you can explain when to use EBS vs S3 vs EFS and design around AZ/Region failures correctly, you’re in good shape for the exam.
  </p>

</section>