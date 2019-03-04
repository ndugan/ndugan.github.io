--- 
title: "Filtering VPC FlowLogs in CloudWatch" 
published: true 
categories: [FlowLogs, Troubleshooting, CloudWatch] 
---

Our on prem networks have the ability to troubleshoot networking issues fairly easily with a variety of tools that were designed for these tasks. Trying to troubleshoot these same issues in AWS became a little more of a challenge, but with some understanding of how to filter CloudWatch, it became relatively simple.

First, it came to setting up logging in VPC flow logs on the server you are monitoring. You have to turn on the flow logs from the network interface, and the easiest way to get to that, is by finding your EC2 instance, selecting it in the top pane and the selecting eth0 in the bottom pane. This allow you to click on the Interface ID, prefixed by eni-, then selecting the Flow Log tab. To create a new flow log, you can choose either the Accept, Reject, or All drop down, and CloudWatch gives you the ability to sort through logs easily. We setup log groups in CloudWatch for each of our servers, so I set the new flow log to dump into the log group for the server I am working with. The IAM role needs to have access to write and list to CloudWatch.

```javascript
{
    "Statement": [
        {
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams",
                "logs:PutLogEvents"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```

Opening CloudWatch -> Logs, you see the groups that are assigned to all of the servers. Drilling down into the server you just added your flow log to, you can see the flow log labeled by the Interface ID of the EC2 instance, labeled by eni-<guid>-all if you select all events. Reviewing the logs, it looks like a standard firewall rule listing, and you can search by string, for example, 8.8.8.8 for the IP you are looking for, but that doesn't let you refine the search. It turns out, you are able to filter the query by using the defined column names and assigning the value you are looking to in each field. The query looks like the following.

```
[version, accountid, interfaceid, srcaddr, dstaddr=8.8.8.8, srcport, dstport=80, protocol, packets, bytes, start, end, action, logstatus]
```

There you have it, a refined way to search your flow logs in CloudWatch.

Happy CloudTrails to you.
