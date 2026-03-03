<!-- ===========================================
     Chapter 2 – File Management & Text Processing
     DevOps / Cloud Engineer Study Guide
     =========================================== -->

<section style="font-family: Arial, sans-serif; line-height: 1.65; max-width: 1000px; margin: 0 auto; color:#222;">

  <h1 style="color:#ff9900; margin-bottom:4px;">
    📘 Chapter 2 – File Management & Text Processing
  </h1>

  <p style="margin-top:0;">
    This is where Linux becomes powerful.  
    DevOps work is mostly: reading logs, searching configs, filtering output, transforming text, and managing files safely.
  </p>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <h3 style="margin:0 0 6px; color:#ff9900;">🎯 Goal of This Chapter</h3>
    <ul style="margin:0; padding-left:18px;">
      <li>Master file operations (create, copy, move, delete)</li>
      <li>Search files efficiently</li>
      <li>Process logs like a DevOps engineer</li>
      <li>Understand pipes & command chaining</li>
    </ul>
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">1️⃣ File Management Essentials</h2>

  <h3 style="color:#ff9900;">Create Files & Directories</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
touch file.txt
mkdir new_folder
mkdir -p app/logs/2025
  </pre>

  <p><b>-p</b> creates nested directories safely.</p>

  <h3 style="color:#ff9900;">Copy Files</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
cp file.txt backup.txt
cp -r folder/ backup_folder/
cp -v file.txt /tmp/
  </pre>

  <ul>
    <li><b>-r</b> → recursive (directories)</li>
    <li><b>-v</b> → verbose (show what is copied)</li>
  </ul>

  <h3 style="color:#ff9900;">Move & Rename</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
mv old.txt new.txt
mv file.txt /opt/app/
  </pre>

  <h3 style="color:#ff9900;">Delete (Be Careful)</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
rm file.txt
rm -r folder/
rm -rf folder/
  </pre>

  <div style="background:#ffeaea; border:1px solid #ffb3b3; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>⚠️ Danger:</b> <code>rm -rf</code> deletes without confirmation.  
    In production, double-check <code>pwd</code> before running destructive commands.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">2️⃣ Viewing & Reading Files</h2>

  <h3 style="color:#ff9900;">Basic Viewing</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
cat file.txt
less file.txt
head -20 file.txt
tail -20 file.txt
tail -f app.log
  </pre>

  <p>
    <b>tail -f</b> is critical for live debugging.
  </p>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Real DevOps Use Case:</b>  
    During deployment, monitor logs:
    <code>tail -f /var/log/nginx/error.log</code>
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">3️⃣ Searching Inside Files – grep</h2>

  <p>
    <b>grep</b> is one of the most used commands in DevOps.
  </p>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
grep "error" app.log
grep -i "error" app.log
grep -r "database" /etc/
grep -v "200" access.log
  </pre>

  <ul>
    <li><b>-i</b> → case insensitive</li>
    <li><b>-r</b> → recursive search</li>
    <li><b>-v</b> → invert match</li>
  </ul>

  <h3 style="color:#ff9900;">Count Matches</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
grep -c "ERROR" app.log
  </pre>

  <div style="background:#fff8ee; border:1px solid #ffd8a8; padding:14px 18px; border-radius:10px; margin:16px 0;">
    <b>Interview Tip:</b>  
    Be ready to explain how you would find all 500 errors in a log file.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">4️⃣ Finding Files – find</h2>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
find /var/log -name "*.log"
find / -type f -size +100M 2>/dev/null
find . -type d
  </pre>

  <p>
    <b>2>/dev/null</b> hides permission errors.
  </p>

  <h3 style="color:#ff9900;">Execute on Found Files</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
find . -name "*.tmp" -exec rm {} \;
  </pre>

  <div style="background:#ffeaea; border:1px solid #ffb3b3; padding:14px 18px; border-radius:10px; margin:16px 0;">
    Always test with <code>-print</code> first before deleting.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">5️⃣ Pipes – The Real Power</h2>

  <p>
    A pipe <code>|</code> sends output of one command into another.
  </p>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
ps aux | grep nginx
cat access.log | grep 500 | wc -l
  </pre>

  <p>
    Think of it as a data pipeline.
  </p>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">6️⃣ Sorting & Counting</h2>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sort file.txt
uniq file.txt
sort file.txt | uniq -c
wc -l file.txt
  </pre>

  <h3 style="color:#ff9900;">Example: Top IP Addresses</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
  </pre>

  <p>
    This is real-world log analysis.
  </p>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">7️⃣ Basic sed & awk (Intro Level)</h2>

  <h3 style="color:#ff9900;">Replace Text with sed</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
sed 's/localhost/127.0.0.1/g' file.txt
  </pre>

  <h3 style="color:#ff9900;">Extract Columns with awk</h3>

  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
awk '{print $2}' file.txt
  </pre>

  <div style="background:#f7f9fc; border:1px solid #e6eefc; padding:14px 18px; border-radius:10px; margin:16px 0;">
    Don’t worry if awk feels confusing now.  
    It becomes powerful once you start analyzing logs daily.
  </div>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <!-- ===================================================== -->
  <h2 style="color:#ff9900;">🧪 Mini Lab – Log Investigation</h2>

  <ol>
    <li>Open a log file.</li>
    <li>Count ERROR occurrences.</li>
    <li>Find top 5 IPs.</li>
    <li>Filter only HTTP 500 responses.</li>
  </ol>

  <p>Use combinations of:</p>
  <pre style="background:#0b1020; color:#e8e8e8; padding:12px; border-radius:8px;">
grep
awk
sort
uniq
wc
head
  </pre>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">🎤 Interview Questions</h2>
  <ul>
    <li>How do you find large files on a server?</li>
    <li>How do you count HTTP 500 errors?</li>
    <li>How do you find top IP addresses hitting your server?</li>
    <li>Difference between grep and find?</li>
  </ul>

  <hr style="border:none; border-top:1px solid #eee; margin:20px 0;" />

  <h2 style="color:#ff9900;">✅ Chapter Summary</h2>
  <p>
    You now know how to manage files safely, search efficiently,
    analyze logs, and combine commands using pipes.
    This is the core operational skillset of a DevOps engineer.
  </p>

</section>