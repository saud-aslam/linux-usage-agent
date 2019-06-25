---


---

<h1 id="introduction">Introduction</h1>
<p>Cluster Monitor Agent is an internal tool that monitors the cluster resources. It helps the infrastructure team to keep track of the hardware specifications and resource usages of a Linux cluster. It also helps to persist the data in an RDBMS databse</p>
<h1 id="architecture-and-design">Architecture and Design</h1>
<p>Architecture:<br>
 
<img src="/Host_Server_arch.jpg" alt="Server-host"></p>
<p>Tables:<br>
<code>host_info</code> stores the hardware specification information whereas <code>host_usage</code> stores the resource usages information. There are two scripts written namely, <code>host_info.sh</code>  which collects the host hardware information and then inserts these information to the table host_info in the database. This script is execute once. <code>host_usage.sh</code> collects the current host usage and then insert the data into host_usage table. Crontab is used to trigger this script every minute. <code>init.sql</code> creates a database and two tables</p>
<h1 id="usage">Usage</h1>
<ol>
<li>
<p><code>psql -h localhost -U postgres -W host_agent -f init.sql</code> to execute init.sql</p>
</li>
<li>
<p>host_info.sh  usage:  <code>bash host_info.sh psql_host psql_port db_name psql_user psql_password</code></p>
</li>
</ol>
<ol start="3">
<li>
<p>host_usage.sh  usage:  <code>bash host_usage.sh psql_host psql_port db_name psql_user psql_password</code></p>
</li>
<li>
<p>crontab setup:  <code>* * * * * /home/centos/dev/jrvs/bootcamp/host_agent/scripts/host_usage.sh localhost 5432 host_agent postgres password &gt; /tmp/host_usage.log</code></p>
</li>
</ol>
<h1 id="improvement">Improvement</h1>
<ol>
<li>handle hardware update</li>
<li>improve sql search</li>
<li>normalized sql tables</li>
<li></li>
</ol>

