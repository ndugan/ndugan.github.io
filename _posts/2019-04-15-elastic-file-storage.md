--- 
title: "Storage That Grows With You, Like Stretchy Pants" 
published: true 
categories: [Elastic File Storage, EFS] 
---

Sometimes you create an instance in AWS, and while it's easy to add more storage space to the disk, sometimes you need storage that can expand with you. The best example for why this is needed is our SIEM. AWS provides the concept of an Elastic File System. Just a note, this currently only works in Linux as NTFS isn't supported. 

This requires you to install the Amazon EFS Utils
```
git clone https://github.com/aws/efs-utils

sudo apt-get -y install binutils

./build-deb.sh

sudo apt-get -y install ./build/amazon-efs-utils*deb
```

You can either mount the file system manually:
```
sudo mount -t efs fs-12345678:/ /mnt/efs
```

Or add the entry into /etc/fstab to mount the system automatically:
```
fs-12345678:/ /mnt/efs efs defaults,_netdev 0 0
```

A couple of notes on this process. When the EFS is created, the security group attached to it needs to allow TCP from the EC2 instance to the EFS volume. Another note was DNS was not setup correctly in my Linux instance, so I added an entry in the hosts file on my EC2 instance to resolve the DNS entry for the EFS. After a config change and a reboot, my elastic search instance can now be mounted off the EFS and will expand as needed, just like stretchy pants at Thanksgiving dinner.

Happy CloudTrails to you.