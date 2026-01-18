## Chap2 - IAC Concepts

### Types of IAC tools
- Configuration tools. i.e, ansible, puppet, saltstack. Designed to install softwares on already acquired infrastructure. These tools are idempotent means that performing the same operation multiple times has the same effect as performing it once
- Provisioning tools. Terraform, Cloudformation.
- Server Templating, Docker, Packer, Vagrant. Docker images, AMI etc. Immutable infrastructure, means after creation, the configuration of infra cannot be changed. If we want to change configuration, new infra will be created after replacing older version.