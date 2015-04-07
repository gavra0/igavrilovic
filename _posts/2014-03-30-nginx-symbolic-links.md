---
layout: post
title: Nginx sites-available &amp; sites-enabled
comments: True
---

Common, and good practice, is to keep Nginx per site configuration in
{% highlight bash %}
/etc/nginx/sites-available
{% endhighlight %}

Configuration that are found in 
{% highlight bash %}
/etc/nginx/sites-enabled
{% endhighlight %}
are the ones that are actually deployed. Instead of copying these configurations, it is much easier to create symbolic links. However, when doing so, use absolute paths for source and destination - example:
{% highlight bash %}
sudo ln -s /etc/nginx/sites-available/yoursite /etc/nginx/sites-enabled/yoursite
sudo service nginx reload
{% endhighlight %}

Creating symbolic links with relative paths did not work for me, but this solved the problem.