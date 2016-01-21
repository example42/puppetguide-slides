
# Components of a Puppet architecture

### Tasks we deal with

Definition of the **classes** to be included in each node

Definition of the **parameters** to use for each node

Definition of the configuration **files** provided to the nodes

### Components

**/etc/puppet/manifests/site.pp** - The default manifests loaded by the Master

**ENC** - The (optional) Enternal Node Classifier

**ldap** - (Optional) LDAP backend

**Hiera** - Data key-value backend

**Public modules** - Public shared modules

**Site modules** - Local custom modules




# Where to define classes

The classes to include in each node can be defined on:

**/etc/puppet/manifests/site.pp** - Top or Node scope variables

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
