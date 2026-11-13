# Upgrading NodeJS for CloudFront Lambda@Edge

We use Lambda@Edge with the [IIIF CloudFront distribution](https://github.com/wellcomecollection/platform-infrastructure/tree/main/cloudfront/iiif.wellcomecollection.org) to rewrite paths.

The `cf_edge_dlcs_path_rewrite` lambda is versioned. The stage and test instances are set up in terraform to use whatever the latest version is. The production instance uses a hardcoded version that we update manually once we've tested the change in stage.\
See [https://github.com/wellcomecollection/platform-infrastructure/blob/main/cloudfront/iiif.wellcomecollection.org/terraform/locals.tf](https://github.com/wellcomecollection/platform-infrastructure/blob/main/cloudfront/iiif.wellcomecollection.org/terraform/locals.tf) for the qualified (ie. includes version) lambda ARNs.&#x20;

* &#x20;Make any required code changes to the lambda code

This is vanilla Javascript so in all likelihood it'll work with the new runtime. If you do need to make some code changes, deploy first.&#x20;

Terraform is applied only from `main` after the pull request has merged (see the [change model](../../developer-handbook/change-model.md#terraform)), so this takes two PRs.

* Bump the runtime on the ["aws\_lambda\_function" "dlcs\_path\_rewrite"](https://github.com/wellcomecollection/platform-infrastructure/blob/main/cloudfront/iiif.wellcomecollection.org/terraform/lambda_dlcs_path_rewrite.tf) in a first PR, and merge it once it is approved.
* From an up-to-date `main`, `terraform plan` should show changes to the above lambda: `runtime` and `version`. The lambda is `publish = true` which means the runtime update automatically publishes a new version. Since the stage and test instances are using the latest version, the `lambda_arn`will also change for these instances. Production stays on its hardcoded version.
* `terraform apply` from `main`: the stage and test lambdas are now running with the updated runtime.
* Test&#x20;
* In a second PR, change the `dlcs_path_rewrite_arn_prod` in `locals.tf` to end with the tested version, and merge it once it is approved.
* `terraform apply` from `main`.



