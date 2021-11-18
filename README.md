#  IBM Behavior Analytics Services terraform module

![Verify and release module](https://github.com/cloud-native-toolkit/terraform-ibm-ocp-bas/workflows/Verify%20and%20release%20module/badge.svg)

Deploys IBM Behavior Analytics Services in a RedHat OpenShift Cluster into the kubernetes namspace specified in the bas_projectName variable.  This kubernetes namespace is created automatically.  A cloud file and block storage classes are needed.  

After installation key values output are:

- API KEY
- BAS Endpoint URL
- Grafana URL

## Supported platforms

- OCP 4.6+

## Module dependencies

The module uses the following elements

### Terraform providers

- null - used to run the shell scripts

### Environment

- kubectl - used to apply yaml 

## Suggested companion modules

The module itself requires some information from the cluster and needs a
namespace to be created. The following companion
modules can help provide the required information:

- Cluster - https://github.com/ibm-garage-cloud/terraform-cluster-ibmcloud

## Example usage

```hcl-terraform
module "mas-bas" {
  source = "github.com/cloud-native-toolkit/terraform-ibm-ocp-bas"

  cluster_config_file      = module.cluster.config_file_path
  cluster_type             = module.cluster.platform.type_code
  cluster_ingress_hostname = module.cluster.platform.ingress
  tls_secret_name          = module.cluster.platform.tls_secret
  
  bas_dbpassword=var.mybas_dbpassword
  bas_grafapassword=var.mybas_grafapassword

}
```

