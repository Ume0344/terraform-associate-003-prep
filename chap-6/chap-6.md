## Terraform Commands

1. terraform validate - checks if syntax/configuration of defined resources are correct
2. terraform fmt - to format the files.
3. terraform show - to show human-readbale output from state/plan files.
4. terraform providers - give information of all the providers used in terraform files.
5. terraform output - gives all the outputs mentioned in files.
6. terraform plan - to get the plan of current state of files against deployed infra/state file.
7. terraform refresh - If a resource is created through terraform but has changed manually, we can use this command to sync the state file with reality of that resource.
8. terraform graph - to create a visual representation of resource dependencies in configuration files.
9. terraform state show/rm/list/pull/mv - always use this command to modify statefile, never do it with code editors.
10. terraform state pull - to download the statefile locally from remote storage.
11. terraform state rm <resource_address> - to remove a resource from state file which we dont want to manage through terraform. It only removes it from statefile and does not deytroy resource in reality.
12. terraform state push - to override the remote state file with local state file

## Lifecycle rules
How lifecycpe of resources hsould be managed. This is the block we add inside of resource block.
```
resource aws_instance mars {
    name = mars
    ...

    lifecycle {
        create_before_destroy = true # create a new resource first and then destroy the old one
        prevent_destroy = true # to preventing from deleting resources accidentally. especially databases which we dont want to delete once they are created.
        ignore_changes = [ # tell terraform to ignore chnages to tags and node_count. means terraform will not take any action in case of chnges in tags/node_count in anayways.
            tags,
            node_count
        ]
    }
}
```

## Terraform taint
1. terraform taint <resource_name> - When a resource is marked as tainted, it will be replaced by next terraform apply command. If some resource is corrupted or broken, we can taint it so, next apply replaces it according to configuration described in files.
2. terraform untaint <resource_name> - resource will not be replaced by next apply command.

## Logging
- To enable logs, set `export TF_LOG=TRACE/INFO/DEBUG/WARNING/ERROR`. TRACE is the most verbose log level.
- To persist logs to a file, use `export TF_LOG_PATH=/tmp/terraform.logs`

## terraform import
to bring the existing resource (created by other means i.e, manually) to terraform state.
`terraform import <resource_type>.<resource_name> <attribute>`. It only adds the resource in state file not in configuration files.

## Terraform Workspace
Terraform workspaces allow you to manage multiple instances of the same infrastructure using a single set of configuration files. Each workspace has its own separate state file.
```
terraform/
├── main.tf (same config)
└── terraform.tfstate.d/
    ├── dev/
    │   └── terraform.tfstate
    ├── staging/
    │   └── terraform.tfstate
    └── prod/
        └── terraform.tfstate
```
