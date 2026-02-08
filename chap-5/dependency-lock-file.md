## dependency lock file
- Manage provider versions in terraform to ensure stable and predictable infra deployments.
- To keep track of provider versions used to create the resources.
- It is created as `terraform.lock.hcl` when terraform init is run.
- It is to ensure that every environment running the terraform configuration code ends up being deployed by same version pf provider. 