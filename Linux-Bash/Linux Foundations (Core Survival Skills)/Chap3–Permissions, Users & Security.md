<!-- ===========================================
     Chapter 3 – Permissions, Users & Security
     DevOps / Cloud Engineer Study Guide
     =========================================== -->

<section style="font-family: Arial, sans-serif; line-height: 1.65; max-width: 1000px; margin: 0 auto; color:#222;">

  <h1 style="color:#ff9900; margin-bottom:4px;">
    📘 Chapter 3 – Permissions, Users & Security
  </h1>

  <p style="margin-top:0;">
    This chapter is critical. Most real-world production issues are caused by:
    <br><br>
    ❌ Wrong permissions  
    ❌ Wrong ownership  
    ❌ Running services as root  
    ❌ Exposed SSH access  
  </p>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <h3 style="margin:0 0 6px; color:#ff9900;">🎯 Goal of This Chapter</h3>
    <ul style="margin:0; padding-left:18px;">
      <li>Understand Linux permission model deeply</li>
      <li>Manage users and groups safely</li>
      <li>Understand sudo and least privilege</li>
      <li>Apply basic Linux security best practices</li>
    </ul>
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">1️⃣ Understanding Linux Permissions</h2>

  <h3 style="color:#ff9900;">Permission Structure</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
-rwxr-xr--
  </pre>

  <p>This breaks down as:</p>

  <table style="border-collapse: collapse; width:100%; font-size:14px;">
    <thead>
      <tr style="background:#fff3e0;">
        <th style="border:1px solid #ffd8a8; padding:10px;">Section</th>
        <th style="border:1px solid #ffd8a8; padding:10px;">Meaning</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="border:1px solid #eee; padding:10px;">First character</td>
        <td style="border:1px solid #eee; padding:10px;">File type (- file, d directory)</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;">rwx (1st triplet)</td>
        <td style="border:1px solid #eee; padding:10px;">Owner permissions</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;">r-x (2nd triplet)</td>
        <td style="border:1px solid #eee; padding:10px;">Group permissions</td>
      </tr>
      <tr>
        <td style="border:1px solid #eee; padding:10px;">r-- (3rd triplet)</td>
        <td style="border:1px solid #eee; padding:10px;">Others permissions</td>
      </tr>
    </tbody>
  </table>

  <p>
    <b>r</b> = read (4)  
    <b>w</b> = write (2)  
    <b>x</b> = execute (1)
  </p>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">2️⃣ Numeric (Octal) Permissions</h2>

  <p>
    Numeric permissions are common in DevOps and automation.
  </p>

  <table style="border-collapse: collapse; width:100%; font-size:14px;">
    <thead>
      <tr style="background:#fff3e0;">
        <th style="border:1px solid #ffd8a8; padding:10px;">Number</th>
        <th style="border:1px solid #ffd8a8; padding:10px;">Meaning</th>
      </tr>
    </thead>
    <tbody>
      <tr><td style="border:1px solid #eee; padding:10px;">7</td><td style="border:1px solid #eee; padding:10px;">rwx</td></tr>
      <tr><td style="border:1px solid #eee; padding:10px;">6</td><td style="border:1px solid #eee; padding:10px;">rw-</td></tr>
      <tr><td style="border:1px solid #eee; padding:10px;">5</td><td style="border:1px solid #eee; padding:10px;">r-x</td></tr>
      <tr><td style="border:1px solid #eee; padding:10px;">4</td><td style="border:1px solid #eee; padding:10px;">r--</td></tr>
    </tbody>
  </table>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
chmod 755 script.sh
chmod 644 file.txt
chmod 600 private_key.pem
  </pre>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Important:</b> SSH private keys must have <code>600</code> permission.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">3️⃣ Ownership – chown & chgrp</h2>

  <h3 style="color:#ff9900;">Check Ownership</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
ls -l
  </pre>

  <h3 style="color:#ff9900;">Change Owner</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo chown user file.txt
sudo chown user:group file.txt
sudo chown -R user:group folder/
  </pre>

  <h3 style="color:#ff9900;">Change Group</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo chgrp developers file.txt
  </pre>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Production Tip:</b>  
    Application directories should not be owned by root unless absolutely necessary.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">4️⃣ Users & Groups Management</h2>

  <h3 style="color:#ff9900;">Create User</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo useradd newuser
sudo passwd newuser
  </pre>

  <h3 style="color:#ff9900;">Create System User (for services)</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo useradd -r -s /usr/sbin/nologin myapp
  </pre>

  <ul>
    <li><b>-r</b> → system user</li>
    <li><b>-s</b> → no login shell</li>
  </ul>

  <h3 style="color:#ff9900;">Add User to Group</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo usermod -aG sudo newuser
sudo usermod -aG docker newuser
  </pre>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">5️⃣ sudo & Least Privilege</h2>

  <p>
    <b>sudo</b> allows controlled root access.
  </p>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sudo command
sudo -l
  </pre>

  <div style="background:#ffeaea; border:1px solid #ffb3b3; padding:14px 18px; border-radius:10px; margin:16px 0;">
    Never log in as root directly in production.
  </div>

  <p>
    Principle: <b>Least Privilege</b>  
    Give only the permissions necessary.
  </p>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">6️⃣ File Special Permissions (Advanced Intro)</h2>

  <h3 style="color:#ff9900;">Setuid</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
chmod u+s file
  </pre>

  <h3 style="color:#ff9900;">Sticky Bit (Important for /tmp)</h3>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
chmod +t directory
  </pre>

  <p>
    Sticky bit allows users to delete only their own files in shared directories.
  </p>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">7️⃣ Basic Security Best Practices</h2>

  <ul>
    <li>Disable root SSH login</li>
    <li>Use SSH keys, not passwords</li>
    <li>Restrict file permissions (600 for secrets)</li>
    <li>Run services as non-root users</li>
    <li>Regularly audit sudo access</li>
  </ul>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Cloud Example:</b>  
    In AWS EC2, security groups control network access, but Linux permissions still protect files inside the server.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">🧪 Mini Lab</h2>

  <ol>
    <li>Create a new user.</li>
    <li>Create a directory owned by that user.</li>
    <li>Restrict access to owner only (700).</li>
    <li>Test access from another user.</li>
  </ol>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">🎤 Interview Questions</h2>

  <ul>
    <li>Explain Linux permission model.</li>
    <li>Difference between 755 and 644?</li>
    <li>How would you secure a production server?</li>
    <li>Why should applications not run as root?</li>
  </ul>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">✅ Chapter Summary</h2>

  <p>
    You now understand Linux permissions, ownership, user management, and security basics.
    This knowledge protects production systems and prevents many common outages.
  </p>

</section>