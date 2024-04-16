# Terraform static webiste AWS S3

### Requirements

1) Get Free Amazon account
2) Install Amazon CLI and configured it with you access key and secret key
3) install terraform 

Creating a static website to show case my skill of using terraform and AWS.  

For this showcase I will be utilizing terraform to create the s3 resources and bucket permission to make the bucket public and create the static website.   

To begin I will set up the provider, in the providers.tf file we have configure our provider in this case is AWS provider. 

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

```
Before we begin with the main.tf, we have a variables file in which this file contains variables to use.  In this example with have the bucket name as a variable.  

```
variable bucket_name {
  type        = string
  default     = "em-static-website-bkt"
  description = "This bucket will hold our static websites"
}

```

To create the bucket in Terraform we will use resource and call the aws_s3_bucket resource then name the resource in this case my_s3_bucket is the resource name.  In side of that we have the bucket name hence the var.bucket_name it comes from the vairables.tf.

```
resource "aws_s3_bucket" "my_s3_bucket" {
  bucket = var.bucket_name

}
```

Using terraform you can make a bucket public, assign ACL, make ownership of the bucket and upload files into the bucket all through terraform.  

We can then use github actions to deploy as CI/CD.  