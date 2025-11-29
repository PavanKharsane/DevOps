If you want your website images or files to be accessible to everyone on the internet, you add a bucket policy like

{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}


Give Access to a Specific IAM User or Role

{
  "Effect": "Allow",
  "Principal": { "AWS": "arn:aws:iam::123456789012:user/DevUser" },
  "Action": "s3:*",
  "Resource": "arn:aws:s3:::my-bucket/*"
}


Allow EC2 or Lambda to Read/Write Your Bucket

{
  "Effect": "Allow",
  "Principal": {
    "AWS": "arn:aws:iam::123456789012:role/MyEC2Role"
  },
  "Action": [
    "s3:GetObject",
    "s3:PutObject"
  ],
  "Resource": "arn:aws:s3:::my-bucket/*"
}


Restrict Access to Specific IP Address

{
  "Effect": "Deny",
  "Principal": "*",
  "Action": "s3:*",
  "Resource": "arn:aws:s3:::my-bucket/*",
  "Condition": {
    "NotIpAddress": { "aws:SourceIp": "103.25.56.10/32" }
  }
}


Enforce Only HTTPS Access (No HTTP)

{
  "Effect": "Deny",
  "Principal": "*",
  "Action": "*",
  "Resource": "arn:aws:s3:::my-bucket/*",
  "Condition": {
    "Bool": { "aws:SecureTransport": "false" }
  }
}
