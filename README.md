# tfc-localBackend

## Description
Tf local backend

## Pre-requirements

* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 
* [Terraform cli](https://learn.hashicorp.com/tutorials/terraform/install-cli)

## How to use this repo

- Clone
- Run
- Cleanup

---

### Clone the repo

```
git clone https://github.com/viv-garot/tfc-localBackend
```

### Change directory

```
cd tfc-localBackend
```

### Run

* Create a new branch:

```
git checkout -b <new branch name>
```

_sample_

```
git checkout -b addingcode
Switched to a new branch 'addingcode
```

* Add a main.tf file with below content :

```
resource "null_resource" "helloWorld" {
    provisioner "local-exec" {
        command = "echo hello world"
    }
}
```

* Run terraform init to download the hashicorp null plugin 

```
terraform init
```

_sample_:

```
terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/null...
- Installing hashicorp/null v3.1.0...
- Installed hashicorp/null v3.1.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

* Run terraform apply to create the null resource :

```
terraform apply --auto-approve=true
```

_sample_:

```
terraform apply --auto-approve=true

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # null_resource.helloWorld will be created
  + resource "null_resource" "helloWorld" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.
null_resource.helloWorld: Creating...
null_resource.helloWorld: Provisioning with 'local-exec'...
null_resource.helloWorld (local-exec): Executing: ["/bin/sh" "-c" "echo hello world"]
null_resource.helloWorld (local-exec): hello world
null_resource.helloWorld: Creation complete after 0s [id=4654382437603395363]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

* Check the untracked files reported by git. Observe several files/folder have been created

```
git status
find . | grep -v git
```

_sample_:

```
git status
On branch addingcode
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.terraform.lock.hcl
	.terraform/
	main.tf
	terraform.tfstate

nothing added to commit but untracked files present (use "git add" to track)


find . | grep -v git
.
./terraform.tfstate
./main.tf
./LICENSE
./.terraform
./.terraform/providers
./.terraform/providers/registry.terraform.io
./.terraform/providers/registry.terraform.io/hashicorp
./.terraform/providers/registry.terraform.io/hashicorp/null
./.terraform/providers/registry.terraform.io/hashicorp/null/3.1.0
./.terraform/providers/registry.terraform.io/hashicorp/null/3.1.0/darwin_amd64
./.terraform/providers/registry.terraform.io/hashicorp/null/3.1.0/darwin_amd64/terraform-provider-null_v3.1.0_x5
./README.md
./.terraform.lock.hcl
```

* Create a .gitignore file with the following content :

```
.terraform*
terraform.tfstate*
```

* Add the main.tf and .gitignore file to the repo

```
git add .gitignore main.tf
```

* Commit the files

```
git commit -m "add main.tf and .gitignore"
```

_sample_

```
git commit -m "add main.tf and .gitignore"
[addingcode 49683ae] add main.tf and .gitignore
 2 files changed, 7 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 main.tf
```
 
* Push to the new branch

```
git push origin <new branch name>
```

_sample_

```
git push origin addingcode
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 469 bytes | 469.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'addingcode' on GitHub by visiting:
remote:      https://github.com/viv-garot/tfc-localBackend/pull/new/addingcode
remote:
To https://github.com/viv-garot/tfc-localBackend
 * [new branch]      addingcode -> addingcode
```


* Merge the change in GitHub with a Pull Request


### Cleanup

```
terraform destroy
```

_sample_:

```
terraform destroy
null_resource.helloWorld: Refreshing state... [id=4654382437603395363]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # null_resource.helloWorld will be destroyed
  - resource "null_resource" "helloWorld" {
      - id = "4654382437603395363" -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

null_resource.helloWorld: Destroying... [id=4654382437603395363]
null_resource.helloWorld: Destruction complete after 0s

Destroy complete! Resources: 1 destroyed.
```
