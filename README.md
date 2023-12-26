<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform Module Database
</h1>

<p align="center" style="font-size: 1.2rem;">
    Terraform module to create Digitalocean database service resource on Digitalocean.
     </p>

<p align="center">

<a href="https://github.com/terraform-do-modules/terraform-digitalocean-database/releases/latest">
  <img src="https://img.shields.io/github/release/terraform-do-modules/terraform-digitalocean-database.svg" alt="Latest Release">
</a>
<a href="https://github.com/terraform-do-modules/terraform-digitalocean-database/actions/workflows/tfsec.yml">
  <img src="https://github.com/terraform-do-modules/terraform-digitalocean-database/actions/workflows/tfsec.yml/badge.svg" alt="tfsec">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-APACHE-blue.svg" alt="Licence">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-module-database'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+Module+Database&url=https://github.com/clouddrove/terraform-module-database'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+Module+Database&url=https://github.com/clouddrove/terraform-module-database'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards strategies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure.

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies:
- [Terraform 1.5.4](https://learn.hashicorp.com/terraform/getting-started/install.html)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-module-database/releases).


Here are examples of how you can use this module in your inventory structure:
### basic example
```hcl
    module "mysql" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "redis"
    cluster_version              = "6"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    redis_eviction_policy        = "volatile_lru"
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "192.168.1.1"
      }
    ]
  }
```
## complete example
```hcl
    module "mysql" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "mysql"
    cluster_version              = "8"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    mysql_sql_mode               = "ANSI,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION,NO_ZERO_DATE,NO_ZERO_IN_DATE,STRICT_ALL_TABLES,ALLOW_INVALID_DATES"
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    databases = ["testdb"]

    users = [
      {
        name              = "test",
        mysql_auth_plugin = "mysql_native_password"
      }
    ]

    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "0.0.0.0"
      }
    ]
  }
```
## mongodb example
```hcl
    module "mongodb" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "mongodb"
    cluster_version              = "6"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    databases = ["testdb"]
    users = [
      {
        name = "test"
      }
    ]

    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "0.0.0.0"
      }
    ]
  }
```
## mysql example
```hcl
    module "mysql" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "mysql"
    cluster_version              = "8"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    mysql_sql_mode               = "ANSI,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION,NO_ZERO_DATE,NO_ZERO_IN_DATE,STRICT_ALL_TABLES,ALLOW_INVALID_DATES"
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    databases = ["testdb"]

    users = [
      {
        name              = "test",
        mysql_auth_plugin = "mysql_native_password"
      }
    ]

    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "0.0.0.0"
      }
    ]
  }
```
## postgresql example
```hcl
    module "postgresql" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "pg"
    cluster_version              = "15"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    databases = ["testdb"]
    users = [
      {
        name = "test"
      }
    ]

    create_pools = true
    pools = [
      {
        name    = "test",
        mode    = "transaction",
        size    = 10,
        db_name = "testdb",
        user    = "test"
      }
    ]

    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "0.0.0.0"
      }
    ]
  }
```
## redis example
```hcl
    module "redis" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "redis"
    cluster_version              = "6"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    redis_eviction_policy        = "volatile_lru"
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "192.168.1.1"
      }
    ]
  }
```
## database replica example
```hcl
    module "redis" {
    source                       = "terraform-do-modules/database/digitalocean"
    version                      = "1.0.0"
    name                         = "app"
    environment                  = "test"
    region                       = "blr1"
    cluster_engine               = "mysql"
    cluster_version              = "8"
    cluster_size                 = "db-s-1vcpu-1gb"
    cluster_node_count           = 1
    cluster_private_network_uuid = module.vpc.id
    mysql_sql_mode               = "ANSI,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION,NO_ZERO_DATE,NO_ZERO_IN_DATE,STRICT_ALL_TABLES,ALLOW_INVALID_DATES"
    cluster_maintenance = {
      maintenance_hour = "02:00:00"
      maintenance_day  = "saturday"
    }
    databases = ["testdb", "testdbt"]

    users = [
      {
        name              = "test1",
        mysql_auth_plugin = "mysql_native_password"
      }
    ]

    ## database replica
    replica_enable = true

    create_firewall = false
    firewall_rules = [
      {
        type  = "ip_addr"
        value = "0.0.0.0"
      }
    ]
  }
```






## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| backup\_restore | The day and the start hour of the maintenance window policy | `map(string)` | `null` | no |
| cluster\_engine | Database engine used by the cluster (ex. pg for PostreSQL, mysql for MySQL, redis for Redis, or mongodb for MongoDB) | `string` | `""` | no |
| cluster\_maintenance | The day and the start hour of the maintenance window policy | `map(string)` | `null` | no |
| cluster\_node\_count | Number of nodes that will be included in the cluster | `number` | `1` | no |
| cluster\_private\_network\_uuid | The ID of the VPC where the database cluster will be located | `string` | `null` | no |
| cluster\_size | Database Droplet size associated with the cluster (ex. db-s-1vcpu-1gb) | `string` | `"db-s-1vcpu-1gb"` | no |
| cluster\_version | The version of the cluster | `string` | `""` | no |
| create\_firewall | Controls if firewall should be created | `bool` | `false` | no |
| create\_pools | Controls if pools should be created | `bool` | `false` | no |
| databases | A list of databases in the cluster | `list(string)` | `[]` | no |
| enabled | Flag to control the resources creation. | `bool` | `true` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| firewall\_rules | List of firewall rules associated with the cluster | `list(map(string))` | `[]` | no |
| label\_order | Label order, e.g. `name`,`application`. | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| managedby | ManagedBy, eg 'terraform-do-modules' or 'hello@clouddrove.com' | `string` | `"terraform-do-modules"` | no |
| mysql\_sql\_mode | A comma separated string specifying the SQL modes for a MySQL cluster. | `string` | `null` | no |
| name | Name  (e.g. `app` or `cluster`). | `string` | `""` | no |
| pools | A list of connection pools in the cluster | `list(map(string))` | `null` | no |
| project\_id | The ID of the project that the database cluster is assigned to. If excluded when creating a new database cluster, it will be assigned to your default project. | `string` | `null` | no |
| redis\_eviction\_policy | A string specifying the eviction policy for a Redis cluster. Valid values are: noeviction, allkeys\_lru, allkeys\_random, volatile\_lru, volatile\_random, or volatile\_ttl | `string` | `null` | no |
| region | DigitalOcean region where the cluster will reside | `string` | `null` | no |
| replica\_enable | Flag to control the resources creation. | `bool` | `false` | no |
| replica\_region | DigitalOcean region where the replica will reside | `string` | `null` | no |
| replica\_size | Database Droplet size associated with the replica (ex. db-s-1vcpu-1gb). Note that when resizing an existing replica, its size can only be increased. Decreasing its size is not supported. | `string` | `"db-s-1vcpu-1gb"` | no |
| users | A list of users in the cluster | `list(map(string))` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| connection\_pool\_host | The hostname used to connect to the database connection pool |
| connection\_pool\_id | The ID of the database connection pool |
| connection\_pool\_password | Password for the connection pool's user |
| connection\_pool\_port | Network port that the database connection pool is listening on |
| connection\_pool\_private\_host | Same as pool host, but only accessible from resources within the account and in the same region |
| connection\_pool\_private\_uri | Same as pool uri, but only accessible from resources within the account and in the same region |
| connection\_pool\_uri | The full URI for connecting to the database connection pool |
| database\_cluster\_default\_database | Name of the cluster's default database |
| database\_cluster\_default\_password | Password for the cluster's default user |
| database\_cluster\_default\_user | Username for the cluster's default user |
| database\_cluster\_host | The hostname of the database cluster |
| database\_cluster\_id | The id of the database cluster |
| database\_cluster\_port | Network port that the database cluster is listening on |
| database\_cluster\_private\_host | Same as host, but only accessible from resources within the account and in the same region |
| database\_cluster\_uri | The full URI for connecting to the database cluster |
| database\_cluster\_urn | The uniform resource name of the database cluster |
| database\_firewall\_id | A unique identifier for the firewall |
| database\_firewall\_rule | A map with rule's uuid, type, value and created\_at params |
| database\_replica\_firewall\_rule | A map with rule's uuid, type, value and created\_at params |
| db\_name | The name for the database |
| replica\_cluster\_default\_database | Name of the replica's default database. |
| replica\_cluster\_default\_password | Password for the replica cluster's default user |
| replica\_cluster\_default\_user | Username for the replica cluster's default user |
| replica\_cluster\_port | Network port that the database replica is listening on. |
| replica\_cluster\_private\_host | Same as host, but only accessible from resources within the account and in the same region. |
| replica\_cluster\_uri | The full URI for connecting to the database replica. |
| replica\_host\_name | The ID of the database replica created by Terraform. |
| replica\_id | The ID of the database replica created by Terraform. |
| user\_password | Password for the database user |
| user\_role | Role for the database user |




## Testing
In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system.

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-module-database/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-module-database)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=
