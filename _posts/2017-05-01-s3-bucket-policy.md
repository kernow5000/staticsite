---
layout: post
title: Open S3 Bucket Policy
description: "A Bucket Policy open to everyone"
modified: 2017-05-01
tags: [ aws, s3, iam, bucket ]
---

I forgot to mention this earlier in a post about how this site is set up, but in order to host
a site on S3, or have acces to files, you will need to apply an S3 Bucket Policy to the bucket. 

In this Policy, which is just JSON, and is related to the part of Amazon Web Services I probably
least understand which is IAM. I can't even remember what is stands for. 

Anyway, you can lock down S3 buckets to certain IP addresses with this JSON policy, which you
can apply to the bucket in the frontend. 

Here's one you can use which is for access *by everyone on the internet*

```json 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mybucketname/*"
        }
    ]
}
```

Replace *mybucketname* with the alias to your S3 bucket. So in this case mine would be
*shaunb.co.uk*

You should be able to get to the files in this bucket from anywhere now. 

Be careful! 


