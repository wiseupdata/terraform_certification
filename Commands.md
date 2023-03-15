# 1. Firsts tests - Complete empty terraform directory 👀️

Directory:

![](assets/20230315_110654_image.png)

## Let's test some commands and see the behaviors ❤️

Version used int the examples:

![](assets/20230315_124414_image.png)

#### The following commands do not generate errors!

```
terraform validate
```

* zero errors!

![](assets/20230315_110822_image.png)

```
terraform init
```

* No errors!

![](assets/20230315_110909_image.png)

```
terraform show
```

* No errors!

![](assets/20230315_110941_image.png)

#### The following commands generates errors!👀️

```
terraform plan
```

* Generate error!
* Not creates the terraform.tfstate

![](assets/20230315_111223_image.png)

```
terraform apply
```

* Generate errors
* Not creates the terraform.tfstate

![](assets/20230315_111319_image.png)

#### The following command do not generate errors and has a very interesting behavior.🚀️

```
terraform destroy
terraform apply -destroy
```

* No errors
* Creates the terraform.tfstate

![](assets/20230315_111511_image.png)

![](assets/20230315_111545_image.png)

# 2. New tests - Single resource no providers

![](assets/20230315_124838_image.png)

#### Let's test the same commands, but now they will return errors! 👀️

```
terraform validate
```

- This time the validate return a error, different when the directory was empty

![](assets/20230315_125059_image.png)

```
terraform destroy
```

- Destroy also does not work anymore.

![](assets/20230315_125533_image.png)

#### Let's pay attention for the following code. Now the Azure provider will be installed, but we did not define nothing apart the resource! 👀️

check the directory before the init:
![](assets/20230315_124838_image.png)

single.tf

```
resource "azurerm_resource_group" "this" {
  name     = "rg-single-resource"
  location = "ukwest"
}
```

#### Let's run the init with this only file, only config.👀️

```
terraform init
```

- The plugging it will be download automatic!
- The lock file will be created automatic!

![](assets/20230315_130644_image.png)

#### Let's look to the directory.

![](assets/20230315_130908_image.png)

> Oh, everything look good, evedon we do not have any provider blocks, or required_proders, nothing.😕

Let's try to created the resource group in Azure, just to let you know we are logged with  `az cli`

```
terraform apply -auto-approve
```

![](assets/20230315_131904_image.png)

- Okay, for Azure a feature block is required, lets add it
