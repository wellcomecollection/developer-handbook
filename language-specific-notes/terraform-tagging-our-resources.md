# Terraform: tagging our resources

We tag our resources with a link to the Terraform configuration in GitHub using the [default tags feature](https://www.hashicorp.com/blog/default-tags-in-the-terraform-aws-provider) in the Terraform provider:

```hcl
provider "aws" {
  region = "eu-west-1"

  default_tags {
    tags = {
      TerraformConfigurationURL = "https://github.com/wellcomecollection/catalogue-pipeline/tree/main/reindexer/terraform"
    }
  }
}
```

These tags are visible in the AWS console, which means you can find a resource in the console and then find exactly where it's defined in Terraform:

<figure><img src="../.gitbook/assets/Screenshot 2023-03-09 at 11.29.14.png" alt="Screenshot of a table of tags in the AWS console. The tags are key-value pairs; the table has one tag. The key is TerraformConfigurationURL and the value is a URL to a specific subfolder of a GitHub repository."><figcaption></figcaption></figure>
