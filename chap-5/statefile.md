## Statefile

- When terraform apply command is run for very first time, statefile is created. `terraform.tfstate` and `terraform.tfstate.backup`.
- This file contains json objects, this file is considered as single source of truth.
- Before terraform apply command, terraform reads statefile, refreshes the state against real infrastructure. If there are some manual changes to resources created by terraform, it will add those to statefile and then produce plan against refreshed statefile and configuration files.
- If we dont want to refresh the statefile, we can do `terraform apply refresh=false`.
- statefiles are madatory for terraform to work.
- statefile also keeps track of dependencies of resources.
- statefiles contains sensitive data, so we need to store it in secure remote state backends like s3, azure storage accounts.
- NEVER change statefiles manually.