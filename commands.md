# 1. Firsts tests - Complete empty terraform directory 👀️

Directory:

![](assets/20230315_110654_image.png)

## Let's test some commnd and see the behaviors ❤️

### The follwing commands do not gernerate erros!

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

* No erros!

![](assets/20230315_110941_image.png)

### The following commands generates errors!👀️ 

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

### The following command do not generate errors and has a very interinting behavior.🚀️ 

```
terraform destroy
terraform apply -destroy
```

* No errors
* Creates the terraform.tfstate

![](assets/20230315_111511_image.png)

![](assets/20230315_111545_image.png)



# 2. New tests - Only one simple resource in one file TF
