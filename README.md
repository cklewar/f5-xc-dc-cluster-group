# F5-XC-DC-CLUSTER-GROUP

This repository consists of Terraform templates to create a F5XC DC Cluster Group.

## Usage

- Clone this repo with: `git clone --recurse-submodules https://github.com/cklewar/f5-xc-dc-cluster-group`
- Enter repository directory with: `cd f5-xc-dc-cluster-group`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
- Initialize with: `terraform init`
- Apply with: `terraform apply -auto-approve` or destroy with: `terraform destroy -auto-approve`

### Example Output

```bash
Terraform will perform the following actions:

  # module.dc_cluster_group.volterra_dc_cluster_group.dc_cluster_group will be created
  + resource "volterra_dc_cluster_group" "dc_cluster_group" {
      + description = "My DC Cluster Group"
      + id          = (known after apply)
      + labels      = {
          + "my-dc-group" = "My DC Cluster Group"
        }
      + name        = "f5xc-dcg-01"
      + namespace   = "system"
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

## Create F5XC DC Cluster Group

```hcl
variable "project_prefix" {
  type        = string
  description = "prefix string put in front of string"
  default = "f5xc"
}

variable "project_suffix" {
  type        = string
  description = "prefix string put at the end of string"
  default = "01"
}

variable "f5xc_api_p12_file" {
  type = string
}

variable "f5xc_api_url" {
  type = string
}

module "dc_cluster_group" {
  source                            = "./modules/f5xc/dc-cluster-group"
  f5xc_dc_cluster_group_name        = format("%s-dcg-%s", var.project_prefix, var.project_suffix)
  f5xc_namespace                    = "system"
  f5xc_api_url                      = var.f5xc_api_url
  f5xc_api_p12_file                 = var.f5xc_api_p12_file
  f5xc_dc_cluster_group_description = "My DC Cluster Group"
  f5xc_dc_cluster_group_labels      = {
    "my-dc-group" : "My DC Cluster Group"
  }
}
```