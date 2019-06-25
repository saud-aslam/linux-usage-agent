---


---

<h1 id="introduction">Introduction</h1>
<p>Cluster Monitor Agent is an internal tool that monitors the cluster resources. It helps the infrastructure team to keep track of the hardware specifications and resource usages of a Linux cluster. It also helps to persist the data in an RDBMS databse</p>
<h1 id="architecture-and-design">Architecture and Design</h1>
<p>Architecture:<br>
<img src="https://www.draw.io/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Untitled%20Diagram.drawio#R5VnLctowFP0aL8vYkh3MkgBpp2lmMmXRZpVRbGGryBYVIph%2BfWWQ%2FAbaDLVdsmF0jx6WzjkXSbYBJ1HykaNV%2BMB8TA1g%2BokBpwYAQ8eWvymwOwC25R6AgBP%2FAFk5MCe%2FsAJNhW6Ij9elhoIxKsiqDHosjrEnShjinG3LzRaMlp%2B6QgGuAXMP0Tr6jfgiPKCuY%2Bb4J0yCUD%2FZMlVNhHRjBaxD5LNtAYIzA044Y%2BJQipIJpil3mpdDv7sjtdnEOI7Fn3SA0%2BXnB%2FL1fhwD634xccZL7%2B6DGuUV0Y1asJqs2GkGONvEPk4HMQ14uw2JwPMV8tLarZRcYqGIqIwsWVTDYS5wcnSeVrZ66RrMIiz4TjbRHVxFmHLMjQq3Of2W5jQsUK%2FbIaV4kI2ckyILipe%2F4Aj0jyOnTFEWd8YR7B9HsEqS3TVJdo2kOeZyjRKzanTJhYsyJ2vB2RJPGGVcIjGLZcvbBaG0AiFKgliGniRKDg5vUxqJ%2FEsbq4qI%2BH76mEYRyjJdQIdRRQZQl8FuUAH8KxXc4yrUTXs1KmR8KhlgxyqMjqsAr1cFWE0Gq2MZgFMjG%2FvyAKRCxkXIAhYjOsvRCi15my%2BMrZQ%2BP7AQO3WaQxvByurhhIjvhfJTOtTAUdE0USPvg50OYrnefaeB6UANPO0By9Fx3ncflTo%2FYk4ka6kNCnqmyz2tpmSHbbiHTx2jlD4C8QCLU3zbzf7gmCJBXsszubjaepp92qaru%2FSonhHDVjPC7TIjzDdlRDEbzMHwXDZc0vj6TnbW%2BLBT4%2FfwngMr95zM5p05f9gf54O3WR%2B0aX3wf1i%2Fh9fX6mHU7dj5Vv36%2BoLW4TMK0gVd7Wn0xjm79bZ6GLWG71IGAMs6NGRDu3eC%2BinxPcgAR5V0aNiP29Whhy%2FVqmeWhpezbqsc1d%2BpPa5%2F0mf%2F5XqNmn1iOCGCcxkRZJh%2FoNjXFb7ywNlv" alt="Server-host"></p>
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
<li></li>
</ol>

