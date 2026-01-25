---
title: IAM Policies
description: This doc page showcases vital IAM Policies.
icon: fontawesome/brands/aws
---

# AWS IAM Policies

#### CloudFront `s3:GetObject` Access Policy
!!! Info
    This policy grants cloudfront access to an exisitng S3 bucket. This is done in order to securly access the bucket contents with out having to expose the bucket to the internet.

```json
{
    "Version": "2008-10-17",
    "Id": "PolicyForCloudFrontPrivateContent",
    "Statement": [
        {
            "Sid": "AllowCloudFrontServicePrincipal",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::{bucket-name}/*",
            "Condition": {
                "StringEquals": {
                    "AWS:SourceArn": "arn:aws:cloudfront::{account-id}:distribution/{distribution-id}"
                }
            }
        }
    ]
}
```

#### Single user S3 Full Access Policy
!!! Info
    This policy grants an IAM user full access to an exisitng S3 bucket.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::{account-id}:user/{user}"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::{bucket-name}",
                "arn:aws:s3:::{bucket-name}/*"
            ]
        }
    ]
}
```