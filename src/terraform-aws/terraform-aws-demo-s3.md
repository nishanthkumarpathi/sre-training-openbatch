# Terraform AWS Demo S3

Step 1: Start with Simple Syntax

```yaml
provider "aws" {
  region = "us-east-1"
}
```

Step 3: Create a Bucket

```yaml
resource "aws_s3_bucket" "bucket" {
  bucket = "terraform-s3-bucket-demo"
}
```

Step 4: Create a Bucket Policy

```yaml
provider "aws" {
  region = "us-east-1"
}

# Create a Bucket and Make it Private Bucket

resource "aws_s3_bucket" "bucket" {
  bucket = "terraform-s3-bucket-demo"
}

resource "aws_s3_bucket_acl" "terraform-s3-bucket-demo-acl" {
  bucket = aws_s3_bucket.bucket.id
  acl    = "private"
}

resource "aws_s3_bucket_policy" "terraform-s3-bucket-demo-policy" {
  bucket = aws_s3_bucket.bucket.id
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Deny",
      "Principal": {
        "AWS": "*"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::terraform-s3-bucket-demo/*"
    }
  ]
}
EOF
}
```


