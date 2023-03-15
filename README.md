# **Terraform Certification🚀️**

Suggestions for passing the exam on your first attempt.❤️

1. Do a good course with plenty of practical examples, and make sure not to skip any of them! (This is very important!
2. Read the documentation guide to the exam. [Associate Review](https://developer.hashicorp.com/terraform/tutorials/certification/associate-review)
3. Practice, practice, practice! The more you work with Terraform, the more comfortable you'll be with its syntax, features, and functionality. Try building out a variety of different infrastructure configurations, and experiment with different providers, modules, and features.
4. Check some commands and interesting behaviors in the [Commands.md](https://github.com/wiseupdata/terraform_certification/blob/main/Commands.md)

## Tips 👀️

- The default number of concurrent operations supported by Terraform apply command is 10 (parallelism)
- Terraform replace is the same of terraform taint
- Each terraform block can contain a number of settings related to Terraform's behavior. Within a terraform block, only constant values can be used; arguments may not refer to named objects such as resources, input variables, etc, and may not use any of the Terraform language built-in functions.
  -A Terraform Enterprise install that is provisioned on a network that does not have Internet access is generally known as an air-gapped install. These types of installs require you to pull updates, providers, etc. from external sources vs. being able to download them directly.
- Terraform Enterprise requires a PostgresSQL for a clustered deployment.
- Some Backends supported: Terraform Enterprise, Consul, S3, Artifactory.
- Terraform Cloud supports the following VCS providers: GitHub, Gitlab, Bitbucket and Azure DevOps
- The existence of a provider plugin found locally in the working directory does not itself create a provider dependency. The plugin can exist without any reference to it in Terraform configuration.
- Function`index` finds the element index for a given value in a list starting with index 0.
- HashiCorp style conventions suggest you that align the equals sign for consecutive arguments for easing readability for configurations
- Infrastructure as Code (IAC) is an approach to infrastructure management that uses code and automation to provision, configure, and manage infrastructure resources.
- IAC allows infrastructure to be treated as software, enabling it to be versioned, tested, and deployed more easily.
- IAC tools like Terraform enable developers and operations teams to define infrastructure in code, reducing the risk of configuration drift and making it easier to manage complex environments.
- In addition to Terraform, other popular IAC tools include Ansible, Puppet, and Chef.
- IAC is becoming increasingly popular in cloud environments, where infrastructure is more dynamic and traditional manual management methods are less efficient.
- provisioner accecpts two types of connections: ssh and winrm

#### Replace

> Using Terraform replace command
> If you want to force replacement of an object even though there are no configuration changes, use the terraform plan or terraform apply command with the -replace option instead. If you are using an older version of Terraform, continue using the terraform taint command. Example:

```
terraform apply -replace=azurerm_resource_group.this -auto-approve
```

* list() it was deprecated and we can use direct the brackets [], tolist still exists

> The list function is no longer available. Prior to Terraform v0.12 it was the only available syntax for writing a literal list inside an expression, but Terraform v0.12 introduced a new first-class syntax.
> To update an expression like list(a, b, c), write the following instead:

```
tolist([a, b, c])
```

> Copy The [ ... ] brackets construct a tuple value, and then the tolist function then converts it to a list. For more information on the value types in the Terraform language, see Type Constraints.

#### Import

1. create the rg in azure.

```
az group list --query "[?name=='rg-import-test']" -o table
az group create --name rg-import-test --location eastus
```

1. create the resource in the config, all requires arguments must be correct.

```
resource "azurerm_resource_group" "import" {
  name = "rg-import-test"
  location = "eastus"
}
```

```
terraform state list

terraform import azurerm_resource_group.import /subscriptions/ff739419-c571-asdfafdfaf53b/resourceGroups/rg-import-test
```

comment the rg in the config manifest and run the apply

```
terraform apply -auto-approve 
```

#### Verbose logging

The bug level staring in the most verbose order:
TRACE, DEBUG, INFO, WARN, ERROR

```
export TF_LOG=TRACE
terraform plan
export TF_LOG=ERROR

export TF_LOG_PROVIDER=TRACE
terraform plan
export TF_LOG_PROVIDER=ERROR

export TF_LOG_PATH=./test
export TF_LOG_PROVIDER=INFO
terraform plan

```

#### Modules:

1. Local paths
2. Terraform Registry
3. GitHub
4. Bitbucket
5. Generic Git, Mercurial repositories
6. HTTP URLs
7. S3 buckets
8. GCS buckets
9. Modules in Package Sub-directories

> Publishing Modules to terraform registry
> Anyone can publish and share modules on the Terraform Registry.
> Published modules support versioning, automatically generate documentation, allow browsing version histories, show examples and READMEs, and more. We recommend publishing reusable modules to a registry.
> Public modules are managed via Git and GitHub. Publishing a module takes only a few minutes. Once a module is published, you can release a new version of a module by simply pushing a properly formed Git tag.
> The registry extracts information about the module from the module's source. The module name, provider, documentation, inputs/outputs, and dependencies are all parsed and available via the UI or API, as well as the same information for any submodules or examples in the module's source repository.

#### Versions

> https://developer.hashicorp.com/terraform/language/modules/syntax#version

* Only public registry, and private can have module versions.

#### Unlock

command used to unlock the locked state file:

```
terraform force-unlock
```

#### Default local backend

> Kind: Enhanced
> The local backend stores state on the local filesystem, locks that state using system APIs, and performs operations locally.

* Terraform standard does not backend type support remote management system.
* The two supported backend types in Terraform are Enhanced Standard

#### Refresh

* Terraform refresh command does updates the state files.

#### Backend block in configuration and best practices for partial configurations

* The way to protect sensitive data with partial configurations are:

1. File: -backend-config=PATH
2. Command-line key/value pairs: config="KEY=VALUE"
3. Interactivly with the commands.

> Querying the Hashicorp Vault is not a option.

#### Dynamic blocks

> * You can dynamically construct repeatable nested blocks like setting using a special dynamic block type, which is supported inside resource, data, provider, and provisioner blocks
> * A dynamic block acts much like a for expression, but produces nested blocks instead of a complex typed value. It iterates over a given complex value, and generates a nested block for each element of that complex value.

#### Built-in dependency management (order of execution based)

* Manage implicit dependencies
  The most common source of dependencies is an implicit dependency between two resources or modules.

#### Vault

* Use Vault as a provider to handle your secrets
* Even using vault the downside of it is the secrets are stored in the state file.

#### Features

* Local manage installation is only available in the Enterprise edition
* Free
  * Workspace manage
  * Private module registry
  * VCS integration
* Paid
  * Team manage and governance

#### Login

* To connect with the Terraform cli cloud is required a token, not a login and password.

# References

1. https://developer.hashicorp.com/terraform/tutorials/certification/associate-review
2. https://developer.hashicorp.com/terraform/tutorials/certification?product_intent=terraform
3. https://www.datocms-assets.com/2885/1602500234-terraform-full-feature-pricing-tablev2-1.pdf
