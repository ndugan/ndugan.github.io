--- 
title: "A DNS Record By Any Other Name" 
published: true 
categories: [DNS, ALB, CNAME, MX, A record] 
---

In redesigning our main website, we decided to make the site fault
tolerant and load balanced. This lead us to using an Application Load Balancer (ALB) in AWS. ALB can act a proxy for the website, along with SSL termination, allowing the SSL cert to be installed on the ALB. It was easy to get the ALB set up and working and add the respective target groups for the web servers.

When it came time to update our DNS records for our top level domain (TLD), we requested to add the CNAME to the DNS entry for the ALB, however, since the URL was for the TLD, and we had a mail record (MX) attached to the TLD, we were only allowed to use an A record. ALBs are not allowed to have Elastic (static) IPs assigned to them, and only can be referenced by DNS name.

Back to the drawing board.

After some searching, I found an article posted by AWS, which lead us through creating an Elastic Load Balancer (ELB), the target groups associated with the ALB, and a lambda function that dynamically updates the targets when the ALBs IP addresses change. The lambda function runs every few minutes, and the first time it runs, it writes a file to an S3 bucket that contains the IPs for the target group, which are the IP addresses of the ALB. On subsequent runs, the file is checked and the ALBs IPs are queried, and if there is a change, the S3 file gets updated along with the target groups.

I won't write out the article again, but here is a [link to the article](https://aws.amazon.com/blogs/networking-and-content-delivery/using-static-ip-addresses-for-application-load-balancers/). 

Happy CloudTrails to you.
