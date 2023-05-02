<h1 align="center">
terraform configuration file to create a CDN with:
</h1>

- s3 bucket

- custom aws managed certficate

- cloudFront

- Route53 DNS entry

How to use:

```
git clone https://github.com/NetBistrotDA/terraform-cdn-bucket-certificate-route53-cloudfront.git
```

set up variables in main.tf:

```tf
provider "aws" {
  region                   = "eu-west-1"
  shared_credentials_files = ["$HOME/.aws/credentials"]
  profile                  = "default"
}

provider "aws" {
  alias                    = "virginia"
  region                   = "us-east-1"
  shared_credentials_files = ["$HOME/.aws/credentials"]
  profile                  = "default"
}

locals {
  bucket_name      = "bucket-name"
  root_domain_name = "domain.com"           
  domain_name      = "subdomain.domain.com"
}
```
For the first provider "aws" you may choose any region.

For the profile field choose according to your [aws cli profile ](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

The "bucket-name" will be created in S3.

The root_domain_name must be in a Route53 hosted zone.

The domain_name will be the prefix for access the cdn objects.

This version considers the April 2023 updated security defaults for new S3 buckets.

See the [issue](https://github.com/hashicorp/terraform-provider-aws/issues/28353).

[Outsource Terraform projects with NetBistrot](https://netbistrot.com/en/outsourcing/)