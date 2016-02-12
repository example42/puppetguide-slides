
# The pieces of our Puppet setup

## What we have to do:

- Define and group the **classes** to include in each node
- Set the **parameters** both global to use for each node
- Manage the **files** used to configure things on our servers

### Available pieces

- **The default_manifest** - The default manifests directory or single site.pp
- **An ENC** - (optional) An External Node Classifier. Can be Puppet Enterprise Console, The Foreman, Puppet Dashboard or any custom solution
- **Hiera** - A hierarchical and modular key-value backend
- **Public modules** - The available universe of public modules
-**Site modules** - Any custom module written for local needs



# Where to define classes

The classes to include in each node can be defined on:

**default_manifest** - Top or Node scope variables

**ENC** - Under the classes key in the provided YAML

**ldap** - puppetClass attribute

**Hiera** - Via the ```hiera_include()``` function

**Site modules** - In roles and profiles or other grouping classes



# Where to define parameters

The classes to include in each node can be defined on:

**/etc/puppet/manifests/site.pp** - Under the node statement

**ENC** - Following the ENC logic

**ldap** - puppetVar attribute

**Hiera** - Via the ```hiera()```, ```hiera_hash()```, ```hiera_array()``` functions of Puppet 3 Data Bindings

**Shared  modules** - OS related settings

**Site modules** - Custom and logical settings

**Facts** - Facts calculated on the client


# Where to define files

**Shared  modules** - Default templates populated via module's params

**Site modules** - All custom static files and templates

**Hiera** - Via the **hiera-file** plugin

**Fileserver** custom mount points
