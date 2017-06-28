# terraform-example

## Installation

[Binary Pckg Here](https://www.terraform.io/downloads.html)

## Add Binary Path
```
// e.g. When terraform binary is in ./Applications directory.
export PATH=${PATH}:/Users/takaki.ishibashi/Applications
```

## Verify
```
$ source ~/.bash_profile
$ terraform
// Show Usage Message
```

## Example(Create for ElasticBeansTalk APP and ENV)
```
// touch example.tf
variable "access_key" {
  default = "<access key value>"
}

variable "secret_key" {
  default = "<secret key value>"
}

provider "aws" {
  access_key = "${var.access_key}"
  secret_key = "${var.secret_key}"
  region = "ap-northeast-1"
}

resource "aws_elastic_beanstalk_application" "example" {
  name = "example-app"
  description = "example-app-desc"
}

resource "aws_elastic_beanstalk_environment" "example" {
  name = "example-env"
  application = "${aws_elastic_beanstalk_application.example.name}"
  solution_stack_name = "64bit Amazon Linux 2017.03 v4.1.0 running Node.js"

  setting {
    namespace = "aws:ec2:vpc"
    name = "VPCID"
    value = "vpc-9308bff7"
  }

  setting {
    namespace = "aws:ec2:vpc"
    name = "Subnets"
    value = "subnet-1b0e736d"
  }
}
```

## Apply
```
$ terraform plan
$ terraform apply
```

## Next
[Learn More for AWS](https://www.terraform.io/docs/providers/aws/index.html)