## Chap3 - Providers

### Providers
- Providers are available in public terraform registry.
- Multiple Providers - Terraform allow us to manage resources from multiple providers in one cofig file. Each provider has to be initialized through `terraform init`.
- Providers naming convention is `{hostname}/{organizationalNamespace}/{type}` i.e, `registry.terraform.io/hashicorp/aws`
- Defining providers argument is to override default configuration of a provider or configuration might use multiple versions of same provider.

### Version Constraints
- To define a specific version of a provider;
```
terraform {
  required_version = ">=1.3.6"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "4.43.0" # here !=, >, < could also be used. i.e, version != "2.2.0, > 1.2.1, <4.0.0"
    }
  }
}
```

- Pessimictic constraint operator (PC=) `~>`, i.e, `~> 1.2` this means terraform can install version `1.2` or any incremental available version i.e, `1.9` (first number of version will remain same as of mentioned in PCO, 1 in this case). another example `~>1.2.2`, terraform can install till `1.2.9` if its is available.

- Aliases - We can create aliases for providers of different configurations. i.e,
```
provider "aws" {
    region = "eu-central-1"
}

provider "aws" {
    region = "us-east-1"
    alias = "east"
}

resource aws_key_pair "alpha" { # will be created in eu-central-1
    key_name = "blablabla"
    public_key = "crocodile"
}

resource aws_key_pair "beta" { # will be created in us-east-1
    key_name = "lion"
    public_key = "monkey"
    provider = aws.east # {provider}.{alias}
}
```

- Version constraints can be used anywhere terraform allows us to specify versions. Most commonly they can be set at:
    - Within the provider version configuration (Inside the required_providers block nested inside the terraform block)
    - The "required_version" argument which is used to set the version of Terraform to use.
    - Within modules. This is where we specify the version of module to be used.
    -  `==` is not a valid operator in version constraints
