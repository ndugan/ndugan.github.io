--- 
title: "Patching Using AWS Systems Manager" 
published: true 
categories: [SSM, Systems Manager] 
---

AWS's System Manager is a powerful tool. You can use it to start a command line remote session on your server, push software and patches to your servers, and manage your instances from the AWS console. AWS has this agent included in most of their base AMIs, but the one thing to be aware of with this is the agent needs the AmazonEC2RoleforSSM IAM role. You can configure this during the creation of the EC2 instance, or if you forget when you create the instance, you can add it later from the "Attach/Replace IAM Role" from the "Instance Settings" context menu. If you add the IAM role, you need to restart the service using the following commands.

```
sudo systemctl stop snap.amazon-ssm-agent.amazon-ssm-agent.service
sudo systemctl start snap.amazon-ssm-agent.amazon-ssm-agent.service

sudo systemctl status snap.amazon-ssm-agent.amazon-ssm-agent.service
```

After the SSM agent is running, it is easy to configure patching for your instances. You can add a maintenance window, for example, weekends after 1PM on Saturday. After you create a maintenance window, you can use the Patch Manager console to select the instances you would like to patch, finding them by tag, patch group or selecting them manually. Patch groups are defined by using a specific tag with the key "Patch Group". Each instance can only have one patch group tag. Amazon has documentation on [how patches are installed.] (https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-how-it-works-installation.html)

It's easy to keep your instances patched using Patch Manager, and the SSM agent comes preinstalled for most AMIs, so there's little reason to have unpatched instances in the cloud.

Happy CloudTrails to you.