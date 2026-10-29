
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Big Data Docker Commands</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f4f7fb;color:#1e293b;line-height:1.6}
header{background:#14213d;color:white;padding:35px 20px;text-align:center}
header h1{margin:0;font-size:30px}
header p{color:#dbeafe}
nav{background:#fff;padding:14px;text-align:center;position:sticky;top:0;box-shadow:0 2px 8px #0001;z-index:5}
nav a{color:#175cd3;text-decoration:none;margin:7px 10px;font-weight:bold;display:inline-block}
main{max-width:950px;margin:25px auto;padding:0 16px}
section{background:white;margin-bottom:24px;padding:24px;border-radius:12px;box-shadow:0 3px 12px #0000000c;scroll-margin-top:100px}
h2{color:#175cd3;margin-top:0}
h3{font-size:16px}
.note{background:#eff6ff;padding:12px;border-left:4px solid #2563eb;border-radius:5px}
.cmd{background:#111827;color:#e5e7eb;padding:16px;border-radius:8px;overflow-x:auto;white-space:pre-wrap;overflow-wrap:anywhere;font-family:Consolas,monospace;font-size:14px}
button{background:#2563eb;color:white;border:0;padding:9px 14px;border-radius:6px;cursor:pointer;margin:8px 0}
button:hover{background:#1d4ed8}
footer{text-align:center;padding:25px;color:#64748b}
</style>
</head>
<body>

<header>
<h1>Big Data Docker Commands</h1>
<p>Quick Reference Guide for Cassandra, Hive, HBase, Hadoop and Pig</p>
</header>

<nav>
<a href="#cassandra">Cassandra</a>
<a href="#hive">Hive</a>
<a href="#hbase">HBase</a>
<a href="#hadoop">Hadoop</a>
<a href="#pig">Pig</a>
</nav>

<main>

<section id="cassandra">
<h2>1. Apache Cassandra</h2>
<p>Start Docker Desktop before running these commands.</p>

<h3>Step 1: Create the container</h3>
<pre class="cmd">docker run -d --name cassandra -p 9042:9042 cassandra:latest</pre>

<h3>Step 2: Start the container</h3>
<pre class="cmd">docker start cassandra</pre>

<h3>Step 3: Enter the CQL shell</h3>
<pre class="cmd">docker exec -it cassandra cqlsh</pre>
<button onclick="copyCmd(this)">Copy commands</button>
</section>

<section id="hive">
<h2>2. Apache Hive</h2>
<p>Start Docker Desktop before running these commands.</p>

<h3>Step 1: Pull the Hive image</h3>
<pre class="cmd">docker pull apache/hive:4.2.1</pre>

<h3>Step 2: Create and run the container</h3>
<pre class="cmd">docker run -d -p 10000:10000 -p 10002:10002 --env SERVICE_NAME=hiveserver2 --name hiveserver2 apache/hive:4.2.1</pre>

<h3>Step 3: Start the container if needed</h3>
<pre class="cmd">docker start hiveserver2</pre>

<h3>Step 4: Enter Beeline</h3>
<pre class="cmd">docker exec -it hiveserver2 beeline -u "jdbc:hive2://localhost:10000/"</pre>

<div class="note">Expected prompt after a successful connection may look like:<br><code>0: jdbc:hive2://localhost:10000/&gt;</code></div>
<button onclick="copyCmd(this)">Copy commands</button>
</section>

<section id="hbase">
<h2>3. Apache HBase</h2>
<p>Clone the HBase repository and build its Docker image.</p>

<h3>Step 1: Clone the repository</h3>
<pre class="cmd">git clone https://github.com/apache/hbase.git</pre>

<h3>Step 2: Open the Docker support folder</h3>
<pre class="cmd">cd hbase\dev-support\hbase_docker</pre>

<h3>Step 3: Build the Docker image</h3>
<pre class="cmd">bash build-hbase.sh --tag master</pre>

<h3>Step 4: Run HBase</h3>
<pre class="cmd">docker run --platform linux/amd64 -it --rm hbase_local</pre>
<button onclick="copyCmd(this)">Copy commands</button>
</section>

<section id="hadoop">
<h2>4. Apache Hadoop</h2>
<p>Check Docker and Docker Compose before setting up Hadoop.</p>

<h3>Step 1: Check Docker</h3>
<pre class="cmd">docker --version
docker compose version
docker info</pre>

<h3>Step 2: Open the Desktop folder in Windows CMD</h3>
<pre class="cmd">cd %USERPROFILE%\Desktop</pre>

<h3>Step 3: Clone the Hadoop Docker repository</h3>
<pre class="cmd">git clone https://github.com/big-data-europe/docker-hadoop.git</pre>

<h3>Step 4: Enter the project folder</h3>
<pre class="cmd">cd docker-hadoop</pre>

<h3>Step 5: Start Hadoop services</h3>
<pre class="cmd">docker compose up -d</pre>

<h3>Step 6: Check running containers</h3>
<pre class="cmd">docker ps</pre>

<h3>Step 7: Check HDFS status</h3>
<pre class="cmd">docker exec -it namenode hdfs dfsadmin -report</pre>
<button onclick="copyCmd(this)">Copy commands</button>
</section>

<section id="pig">
<h2>5. Apache Pig</h2>
<p>Start a container with Hadoop, Spark, Pig and Hive tools.</p>

<h3>Step 1: Run the Docker image</h3>
<pre class="cmd">docker run -it suhothayan/hadoop-spark-pig-hive:2.9.2 bash</pre>

<p>After the container starts, you will enter its Bash terminal.</p>
<button onclick="copyCmd(this)">Copy command</button>
</section>

<section>
<h2>Important Notes</h2>
<ul>
<li>Install and start Docker Desktop before running the Docker commands.</li>
<li>Install Git if you need to clone the repositories.</li>
<li>Run each command in the appropriate terminal, such as Windows CMD, PowerShell, Git Bash or a container shell.</li>
<li>Use <code>docker ps</code> to check running containers.</li>
<li>If a container already exists, you usually do not need to create it again.</li>
</ul>
</section>

</main>

<footer>
<p>Big Data Tools — Docker Command Reference</p>
</footer>

<script>
function copyCmd(button){
  const section=button.closest("section");
  const blocks=section.querySelectorAll("pre.cmd");
  const text=Array.from(blocks).map(b=>b.innerText).join("\n\n");
  navigator.clipboard.writeText(text).then(()=>{
    button.innerText="Copied!";
    setTimeout(()=>button.innerText="Copy commands",1500);
  }).catch(()=>{
    alert("Copy failed. Please select and copy the commands manually.");
  });
}
</script>

</body>
</html>
