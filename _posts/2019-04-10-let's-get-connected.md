--- 
title: "Let's Get Connected" 
published: true 
categories: [AWS, SSH, Linux] 
---

Logging in to an AWS linux server is fairly easy and straight foward, but different than connecting to a Windows server. The first step is making sure the security group allows through the IP or IP range of your subnet on port 22. Remember to only allow through your subnet and NOT 0.0.0.0/0, because port 22 will be attacked frequently when open to the internet.

We will be using PuTTY to connect to SSH. The steps for this process are to find the .pem file used to create the linux instance, convert it to a private key file PuTTY understands and then use it as part of the connection settins in PuTTY. [This link from AWS] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html?icmpid=docs_ec2_console) walks through setting this up. WinSCP is the preferred method for transferring files to the linux instances, as it can use the PuTTY key file used to connect directly to the instance.

Happy CloudTrails to you.