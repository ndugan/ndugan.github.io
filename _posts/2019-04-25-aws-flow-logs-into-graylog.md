--- 
title: "Import AWS Flow Logs Into Graylog" 
published: true 
categories: [FlowLogs, Monitoring, Graylog] 
---

When I started setting up Graylog, I decided to put as much data into it as possible. One of the items I wanted to analyze were the VPC Flow Logs from our AWS environment. I couldn't find a good tutorial online, and most of the documentation on how to get the data out of CloudWatch referenced lambda functions and using the Firehose streams. After some searching, I found that you can add a subscription on a CloudWatch log group directly to a Kinesis stream, which is what Graylog imports from. Currently however, there is no way to add the subscription via the console, you have to add it using the AWS CLI. [AWS has a great tutorial on setting this up,] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs//SubscriptionFilters.html#DestinationKinesisExample) but I spent several hours trying to get it all working. Now that everything is set up, Graylog is receiving flow logs and it is parsing the fields as expected.

Hopefully this helps someone.

Happy CloudTrails to you.