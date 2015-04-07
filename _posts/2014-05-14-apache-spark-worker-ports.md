---
layouy: post
title: Apache Spark Worker Random Port Usage
---

There are pleanty of tutorials how to deploy Spark in different environments e.g. <a href="https://spark.apache.org/docs/latest/ec2-scripts.html">https://spark.apache.org/docs/latest/ec2-scripts.html</a>.

However, if this is suppose to be done with a group of machines that are not part of a single VPN, or just belong to multiple users, this process can be quite cumbersome.

One of the problems I ran into was failure for the Master to communicate with Worker nodes. Master runs on dedicated port (default: 7077), but Workers are ran on a randomly selected port (<a href="https://spark.apache.org/docs/1.3.0/spark-standalone.html#cluster-launch-scripts">https://spark.apache.org/docs/1.3.0/spark-standalone.html#cluster-launch-scripts</a>)

> SPARK_WORKER_PORT: Start the Spark worker on a specific port (default: random).

Check your logs in
{% highlight bash %}
	$SPARK_HOME/work/APP_ID/EXECUTOR_ID/stderr
{% endhighlight %}
just to make sure there is a time out in communication, or that packets are dropped.

Anyhow, what worked for me was allowing TCP on all ports. This is very unsafe, and please try first to run workers on dedicated ports (setting this option did not work for me), and use this as the last solution:
{% highlight bash %}
	sudo ufw allow 1:65535/tcp
{% endhighlight %}
