---
title:  "CoreOS: Get cloud-init from external url"
date:   2016-11-13 15:19:00
description: Dynamically change cloud-init on CoreOS
---

CoreOS use cloud-init instead cloud-config.
The cloud-init is a subset of cloud-config plus several CoreOS-specific options.

The cloud-config run at the first boot, but in CoreOS it run during each boot.

In Cloud provider, like AWS, you need to stop the instance for change the user-data, of course that this make sense when it run only at the first boot but when it run during each boot the ability of change the user-data without stop the instance is very useful.

We can do it using a shell script as user-data and running the cloud-config from this.

{% highlight bash %}
#!/bin/bash
/usr/bin/coreos-cloudinit --from-url=https://yagonobre.com/cloud-init
{% endhighlight %}

I recommend that you put the cloud-init file on s3 and use this script for run the cloud-init 

{% highlight bash %}
#!/bin/bash
region="us-east-1"
bucket="test123"
path="user-data/host"

#Get s3-get-presigned
/usr/bin/curl -L -o /usr/local/bin/s3-get-presigned-url https://github.com/kz8s/s3-get-presigned-url/releases/download/v0.1/s3-get-presigned-url_linux_amd64
/usr/bin/chmod +x /usr/local/bin/s3-get-presigned-url

#Run Cloudinit
/usr/bin/coreos-cloudinit --from-url=$(/usr/local/bin/s3-get-presigned-url ${ region } ${ bucket } ${ path })
{% endhighlight %}

Make sure that the instance have access to the bucket.