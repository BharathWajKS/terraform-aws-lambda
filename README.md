<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS Lambda
</h1>

<p align="center" style="font-size: 1.2rem;">
    Terraform module to create Lambda resource on AWS for create lambda function.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v0.12-green" alt="Terraform">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="Licence">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-aws-lambda'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+AWS+Lambda&url=https://github.com/clouddrove/terraform-aws-lambda'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+AWS+Lambda&url=https://github.com/clouddrove/terraform-aws-lambda'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards stratergies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure.

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies:

- [Terraform 0.12](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)
- [github.com/stretchr/testify/assert](https://github.com/stretchr/testify)
- [github.com/gruntwork-io/terratest/modules/terraform](https://github.com/gruntwork-io/terratest)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-lambda/releases).


Here are some examples of how you can use this module in your inventory structure:
### Basic Function
```hcl
  module "lambda" {
    source         = "git::https://github.com/clouddrove/terraform-aws-lambda.git?ref=tags/0.12.0"
    name           = "lambda"
    application    = "clouddrove"
    environment    = "test"
    label_order    = ["environment", "name", "application"]
    enabled        = true
    filename       = "./../../../lambda_function_payload"
    handler        = "index.handler"
    runtime        = "nodejs8.10"
    variables      = {
                       foo = "bar"
                     }
  }
```
### Basic S3 Function
```hcl
  module "lambda" {
    source        = "git::https://github.com/clouddrove/terraform-aws-lambda.git?ref=tags/0.12.0"
    name          = "lambda"
    application   = "clouddrove"
    environment   = "test"
    label_order   = ["environment", "name", "application"]
    enabled       = true
    s3_bucket     = "test-mysql-backups"
    s3_key        = "lambda_function_payload.zip"
    handler       = "index.handler"
    runtime       = "nodejs8.10"
    variables     = {
                      foo = "bar"
                    }
  }
```
### Complete Function
```hcl
  module "lambda" {
    source               = "git::https://github.com/clouddrove/terraform-aws-lambda.git?ref=tags/0.12.0"
    name                 = "lambda"
    application          = "clouddrove"
    environment          = "test"
    label_order          = ["environment", "name", "application"]
    enabled              = true
    filename             = "./../../../lambda_function_payload"
    handler              = "index.handler"
    runtime              = "nodejs8.10"
    subnet_ids           = ["subnet-xxxxxxxxxxxxxx", "subnet-xxxxxxxxxxxxxx"]
    security_group_ids   = ["sg-xxxxxxxxxxxxxx", "sg-xxxxxxxxxxxxxx"]
    names                = [
                            "lambda_layer_name"
                           ]
    filenames            = [
                            {
                              "input"="./../../../lambda_function_payload",
                              "output"="lambda_function_payload.zip",
                            }
                           ]
    compatible_runtimes  = [
                            ["nodejs8.10"]
                           ]

    statement_ids        = [
                            "AllowExecutionFromSNS"
                           ]
    actions              = [
                            "lambda:InvokeFunction"
                           ]
    principals           = [
                            "sns.amazonaws.com"
                           ]
    source_arns          = [
                            "arn:aws:sns:eu-west-1:xxxxxxxxxxxxxx:test-sns-clouddrove"
                           ]
    variables            = {
                             foo = "bar"
                           }
  }
```






## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| actions | The AWS Lambda action you want to allow in this statement. (e.g. lambda:InvokeFunction). | list | `<list>` | no |
| application | Application (e.g. `cd` or `clouddrove`). | string | `` | no |
| attributes | Additional attributes (e.g. `1`). | list | `<list>` | no |
| compatible_runtimes | A list of Runtimes this layer is compatible with. Up to 5 runtimes can be specified. | list | `<list>` | no |
| delimiter | Delimiter to be used between `organization`, `environment`, `name` and `attributes`. | string | `-` | no |
| description | Description of what your Lambda Function does. | string | `` | no |
| descriptions | Description of what your Lambda Layer does. | list | `<list>` | no |
| enabled | Whether to create lambda function. | bool | `false` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | string | `` | no |
| event_source_tokens | The Event Source Token to validate. Used with Alexa Skills. | list | `<list>` | no |
| filename | The path to the function's deployment package within the local filesystem. If defined, The s3_-prefixed options cannot be used. | string | `` | no |
| filenames | The path to the function's deployment package within the local filesystem. If defined, The s3_-prefixed options cannot be used. | list | `<list>` | no |
| handler | The function entrypoint in your code. | string | - | yes |
| kms_key_arn | The ARN for the KMS encryption key. | string | `` | no |
| label_order | Label order, e.g. `name`,`application`. | list | `<list>` | no |
| layers | List of Lambda Layer Version ARNs (maximum of 5) to attach to your Lambda Function. | string | `` | no |
| license_infos | License info for your Lambda Layer. See License Info. | list | `<list>` | no |
| memory_size | Amount of memory in MB your Lambda Function can use at runtime. Defaults to 128. | number | `128` | no |
| name | Name  (e.g. `app` or `cluster`). | string | `` | no |
| names | A unique name for your Lambda Layer. | list | `<list>` | no |
| principals | The principal who is getting this permission. e.g. s3.amazonaws.com, an AWS account ID, or any valid AWS service principal such as events.amazonaws.com or sns.amazonaws.com. | list | `<list>` | no |
| publish | Whether to publish creation/change as new Lambda Function Version. Defaults to false. | bool | `false` | no |
| qualifiers | Query parameter to specify function version or alias name. The permission will then apply to the specific qualified ARN. e.g. arn:aws:lambda:aws-region:acct-id:function:function-name:2 | list | `<list>` | no |
| reserved_concurrent_executions | The amount of reserved concurrent executions for this lambda function. A value of 0 disables lambda from being triggered and -1 removes any concurrency limitations. Defaults to Unreserved Concurrency Limits -1. | number | `-1` | no |
| runtime | Runtimes. | string | - | yes |
| s3_bucket | The S3 bucket location containing the function's deployment package. Conflicts with filename. This bucket must reside in the same AWS region where you are creating the Lambda function. | string | `` | no |
| s3_buckets | The S3 bucket location containing the function's deployment package. Conflicts with filename. This bucket must reside in the same AWS region where you are creating the Lambda function. | list | `<list>` | no |
| s3_keies | The S3 key of an object containing the function's deployment package. Conflicts with filename. | list | `<list>` | no |
| s3_key | The S3 key of an object containing the function's deployment package. Conflicts with filename. | string | `` | no |
| s3_object_version | The object version containing the function's deployment package. Conflicts with filename. | string | `` | no |
| s3_object_versions | The object version containing the function's deployment package. Conflicts with filename. | list | `<list>` | no |
| security_group_ids | Security group ids for vpc config. | list | `<list>` | no |
| source_accounts | This parameter is used for S3 and SES. The AWS account ID (without a hyphen) of the source owner. | list | `<list>` | no |
| source_arns | When granting Amazon S3 or CloudWatch Events permission to invoke your function, you should specify this field with the Amazon Resource Name (ARN) for the S3 Bucket or CloudWatch Events Rule as its value. This ensures that only events generated from the specified bucket or rule can invoke the function. | list | `<list>` | no |
| statement_ids | A unique statement identifier. By default generated by Terraform. | list | `<list>` | no |
| subnet_ids | Subnet ids for vpc config. | list | `<list>` | no |
| tags | Additional tags (e.g. map(`BusinessUnit`,`XYZ`). | map | `<map>` | no |
| timeout | The amount of time your Lambda Function has to run in seconds. Defaults to 3. | number | `3` | no |
| variables | A map that defines environment variables for the Lambda function. | map | `<map>` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The Amazon Resource Name (ARN) identifying your Lambda Function. |
| tags | A mapping of tags to assign to the resource. |




## Testing
In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system.

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-aws-lambda/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-aws-lambda)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=