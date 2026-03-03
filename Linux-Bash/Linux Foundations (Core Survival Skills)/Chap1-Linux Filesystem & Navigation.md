<!-- ===========================================
     Chapter 1 – Linux Filesystem & Navigation
     DevOps / Cloud Engineer Study Guide
     =========================================== -->

<section style="font-family: Arial, sans-serif; line-height: 1.65; max-width: 1000px; margin: 0 auto; color:#222;">

  <h1 style="color:#ff9900; margin-bottom: 4px;">
    📘 Chapter 1 – Linux Filesystem & Navigation
  </h1>
  <p style="margin-top:0;">
    This chapter builds your foundation. Every DevOps or Cloud Engineer must be completely comfortable navigating Linux systems.
    If you can’t move confidently inside a server, debugging and automation become painful.
  </p>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <h3 style="margin:0 0 6px; color:#ff9900;">🎯 Goal of This Chapter</h3>
    <ul style="margin:0; padding-left:18px;">
      <li>Understand Linux directory structure</li>
      <li>Navigate efficiently in production servers</li>
      <li>Understand absolute vs relative paths</li>
      <li>Develop safe operational habits</li>
    </ul>
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">1️⃣ Linux Filesystem Hierarchy</h2>

  <p>
    Linux uses a <b>single root hierarchy</b>. Everything starts from:
  </p>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">/</pre>

  <p>
    Unlike Windows (C:, D: drives), Linux organizes everything under one root tree.
    Even mounted disks attach somewhere inside this tree.
  </p>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>DevOps Insight:</b> When troubleshooting storage issues in cloud environments (AWS EC2, Azure VM),
    new disks are mounted somewhere inside <code>/</code>, not as new drive letters.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">2️⃣ Important Directories (Production-Relevant)</h2>

  <table style="border-collapse: collapse; width:100%; font-size:14px;">
    <thead>
      <tr style="background:#fff3e0;">
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Directory</th>
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Purpose</th>
        <th style="border:1px solid #ffd8a8; padding:10px; text-align:left;">Why It Matters</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/etc</code></td>
        <td style="border:1px solid #eee; padding:10px;">System configuration</td>
        <td style="border:1px solid #eee; padding:10px;">nginx.conf, sshd_config, environment configs</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/var</code></td>
        <td style="border:1px solid #eee; padding:10px;">Variable runtime data</td>
        <td style="border:1px solid #eee; padding:10px;">Logs, cache, database files</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/var/log</code></td>
        <td style="border:1px solid #eee; padding:10px;">System & app logs</td>
        <td style="border:1px solid #eee; padding:10px;">Debugging production issues</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/home</code></td>
        <td style="border:1px solid #eee; padding:10px;">User directories</td>
        <td style="border:1px solid #eee; padding:10px;">SSH keys, user files</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/opt</code></td>
        <td style="border:1px solid #eee; padding:10px;">Optional software</td>
        <td style="border:1px solid #eee; padding:10px;">Custom app deployments</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/tmp</code></td>
        <td style="border:1px solid #eee; padding:10px;">Temporary files</td>
        <td style="border:1px solid #eee; padding:10px;">Short-lived debugging files</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;"><code>/proc</code></td>
        <td style="border:1px solid #eee; padding:10px;">Kernel & process info</td>
        <td style="border:1px solid #eee; padding:10px;">CPU, memory inspection</td>
      </tr>
    </tbody>
  </table>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">3️⃣ Navigation Commands</h2>

  <h3 style="color:#ff9900;">Show Current Directory</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">pwd</pre>

  <h3 style="color:#ff9900;">List Files Properly</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">ls -lah</pre>

  <p>
    Always prefer <code>-lah</code> in production:
  </p>
  <ul>
    <li><b>-l</b> → detailed view</li>
    <li><b>-a</b> → hidden files</li>
    <li><b>-h</b> → human readable sizes</li>
  </ul>

  <h3 style="color:#ff9900;">Change Directory</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
cd /var/log
cd ..
cd ~
  </pre>

  <p>
    Shortcuts:
  </p>
  <ul>
    <li><code>~</code> → home directory</li>
    <li><code>.</code> → current directory</li>
    <li><code>..</code> → parent directory</li>
  </ul>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">4️⃣ Absolute vs Relative Paths</h2>

  <h3 style="color:#ff9900;">Absolute Path</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">/var/log/nginx/access.log</pre>

  <h3 style="color:#ff9900;">Relative Path</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">../logs/access.log</pre>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>DevOps Rule:</b> In automation scripts, always prefer absolute paths.
    Relative paths break in cron jobs and CI/CD pipelines.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">5️⃣ Viewing File Details</h2>

  <h3 style="color:#ff9900;">File Metadata</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">stat file.txt</pre>

  <h3 style="color:#ff9900;">Check File Type</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">file file.txt</pre>

  <h3 style="color:#ff9900;">Sort by Size or Time</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
ls -lhS   # sort by size
ls -lt    # sort by modification time
  </pre>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">6️⃣ Safe Production Habits</h2>

  <p>
    Every time you SSH into a server:
  </p>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
whoami
pwd
ls -lah
  </pre>

  <ul>
    <li>Confirm your user</li>
    <li>Confirm your location</li>
    <li>Inspect surroundings before modifying anything</li>
  </ul>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Professional Insight:</b> Many outages happen because someone ran a command in the wrong directory.
    Awareness prevents accidents.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">🧪 Mini Lab</h2>

  <ol>
    <li>SSH into a Linux server.</li>
    <li>Navigate to <code>/var/log</code>.</li>
    <li>Find the largest file:</li>
  </ol>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">ls -lhS</pre>

  <ol start="4">
    <li>Find most recently modified file:</li>
  </ol>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">ls -lt</pre>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">🎤 Interview Questions You Must Answer</h2>
  <ul>
    <li>What is root <code>/</code> in Linux?</li>
    <li>Difference between <code>/etc</code> and <code>/var</code>?</li>
    <li>What happens if <code>/var</code> becomes full?</li>
    <li>Why are logs stored under <code>/var/log</code>?</li>
  </ul>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">✅ Chapter Summary</h2>
  <p>
    You now understand Linux directory structure, navigation commands, path types,
    and safe operational habits. This is the foundation for debugging, automation,
    and production-level system management.
  </p>

</section>