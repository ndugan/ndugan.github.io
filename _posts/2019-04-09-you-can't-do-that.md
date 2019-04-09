--- 
title: "You Can't Do That!" 
published: true 
categories: [Port25, SMTP] 
---

Occasionally, you'll have an application that also sends email as part of it's normal function. When we migrated several of our application servers, we noticed some odd behavior with the servers. We couldn't send email from them anymore. Testing the application lead us to try telnet on port 25 to the mail server we were connecting to. It seemed to work sporadically at best. Reviewing the VPC flow logs, I noticed that port 25 was being rejected outbound. Since the server allowed all traffic out, I wrote a security group to try to force port 25 open to the server I was connecting to. This did not fix the issue, so a quick search directed me to [this article.] (https://aws.amazon.com/premiumsupport/knowledge-center/ec2-port-25-throttle/) 

The summary of the article above is that you need to have a DNS entry for the server you would like to allow to send on port 25 and then submit a request to AWS using your root account to remove throttling from your instance. I can understand why AWS would restrict this, however, I wish it had been more clear they do this by default before spending days troubleshooting this issue.

Happy CloudTrails to you.