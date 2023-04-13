# AWS VPC Endpoints Terraform module

## ⚠️ Module is deprecated in favor of upstream VPC module

This module was created temporarily to demonstrate how to create a scalable VPC endpoint module. This functionality has been merged into the upstream [`terraform-aws-vpc`](https://github.com/terraform-aws-modules/terraform-aws-vpc) module.

Users can change their module source to continue to utilize this functionality from the upstream VPC module:

```diff
- source = "clowdhaus/vpc-endpoints/aws"
+ source = "terraform-aws-modules/vpc/aws//modules/vpc-endpoints"
```

Terraform module which creates VPC endpoint resources on AWS.

## Usage

See [`examples`](./examples) directory for working examples to reference:

```hcl
module "endpoints" {
  source  = "git::https://git@github.com/ahmadzaikk/terraform-aws-vpc-endpoints.git"

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

## Examples

Examples codified under the [`examples`](./examples) are intended to give users references for how to use the module(s) as well as testing/validating changes to the source code of the module(s). If contributing to the project, please be sure to make any appropriate updates to the relevant examples to allow maintainers to test your changes and to keep the examples up to date for users. Thank you!

- [Complete](./examples/complete)

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.1 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 3.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_vpc_endpoint.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc_endpoint) | resource |
| [aws_vpc_endpoint_service.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/vpc_endpoint_service) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_endpoints"></a> [endpoints](#input\_endpoints) | A map of interface and/or gateway endpoints containing their properties and configurations | `any` | `{}` | no |
| <a name="input_security_group_ids"></a> [security\_group\_ids](#input\_security\_group\_ids) | Default security group IDs to associate with the VPC endpoints | `list(string)` | `[]` | no |
| <a name="input_subnet_ids"></a> [subnet\_ids](#input\_subnet\_ids) | Default subnets IDs to associate with the VPC endpoints | `list(string)` | `[]` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | A map of tags to use on all resources | `map(string)` | `{}` | no |
| <a name="input_timeouts"></a> [timeouts](#input\_timeouts) | Define maximum timeout for creating, updating, and deleting VPC endpoint resources | `map(string)` | `{}` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The ID of the VPC in which the endpoint will be used | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_endpoints"></a> [endpoints](#output\_endpoints) | Array containing the full resource object and attributes for all endpoints created |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## License

Apache-2.0 Licensed. See [LICENSE](LICENSE).
