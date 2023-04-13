# AWS VPC Endpoints Terraform module


Terraform module which creates VPC endpoint resources on AWS.

## Usage


```hcl
module "endpoints" {
  source  = "git::https://git@github.com/ucopacme/terraform-aws-vpc-endpoints.git"

  vpc_id             = "vpc-09090"
  security_group_ids = ["sg-04bd09090"]

  endpoints = {
    s3 = {
      service             = "s3"
      service_type    = "Gateway"
      route_table_ids = ["rtb-07ba7209090"]
      private_dns_enabled = true
      tags                = { Name = "s3-vpc-endpoint" }
    },
    ecr = {
      service         = "ecr.dkr"
      subnet_ids          = ["subnet-12345678", "subnet-87654321"]
      # service_type    = "Interface"
      security_group_ids  = ["sg-04b09090"]
      tags            = { Name = "ecr-vpc-endpoint" }
    },
    ecrapi = {
      service         = "ecr.api"
      subnet_ids          = ["subnet-12345678", "subnet-87654321"]
      # service_type    = "Interface"
      security_group_ids  = ["sg-04bd8230659cddc48"]
      tags            = { Name = "ecr-vpc-endpoint" }
    },
    logs = {
      service         = "logs"
      subnet_ids          = ["subnet-12345678", "subnet-87654321"]
      # service_type    = "Interface"
      security_group_ids  = ["sg-04bd8230659cddc48"]
      tags            = { Name = "ecr-vpc-endpoint" }
    }
    sns = {
      service    = "sns"
      subnet_ids = ["subnet-12345678", "subnet-87654321"]
      tags       = { Name = "sns-vpc-endpoint" }
    },
    sqs = {
      service             = "sqs"
      private_dns_enabled = true
      security_group_ids  = ["sg-987654321"]
      subnet_ids          = ["subnet-12345678", "subnet-87654321"]
      tags                = { Name = "sqs-vpc-endpoint" }
    },
  }

  tags = {
    Owner       = "user"
    Environment = "dev"
  }
}
```

