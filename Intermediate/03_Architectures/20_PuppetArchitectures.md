# Puppet architectures - Overview

### The Components of a Puppet architecture

### Where to define classes

### Where to define parameters

### Where to place files

### Puppet security



# Components of a Puppet architecture

### Tasks we deal with

Definition of the **classes** to be included in each nodeDefinition of the **parameters** to use for each nodeDefinition of the configuration **files** provided to the nodes

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


# Nodes - Default classification

A node is identified by the PuppetMaster by its **certname**, which defaults to the node's **fqdn**

In the first manifest file parsed by the Master, ```site.pp```, we can define nodes with a syntax like:

    node 'web01' {
      include apache
    }

We can also define a list of matching names:

    node 'web01' , 'web02' , 'web03' {
      include apache
    }

or use a regular expression:

    node /^www\d+$/ {
      include apache
    }

A node can inherit another node and include all the classes and variables defined for it, this feature is now deprecated and is not supported anymore on Puppet 4.


# Nodes classification via an ENC

Puppet can query an external source to retrieve the classes and the parameters to assign to a node. This source is called External Node Classifier (ENC) and can be anything that, when interrogated via a script with the clients' certname as first parameter, returns a yaml file with the list of classes and parameters.

Common ENC are **Puppet DashBoard**, **The Foreman** and **Puppet Enterprise** (where the functionality of ENC is enabled by default).

To enable the usage of an ENC set these parameters in ```puppet.conf```

    # Enable the usage of a script to classify nodes
    node_terminus = exec

    # Path of the script to execute to classify nodes
    external_nodes = /etc/puppet/node.rb

# Nodes classification with Hiera

Hiera provides a **hiera_include** function that allows the inclusion of classes as defined on Hiera. This is an approach that can be useful when there's massive usage of Hiera as backend for Puppet data.

In ```/etc/puppet/manifests/site.pp``` just place:

    hiera_include('classes')

and place, as an array, the classes to include in our Hiera data source under the key ```classes```.




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


# Puppet Security considerations

  Client / Server communications are encrypted with SSL x509 certificates
  By default the CA on the PuppetMaster requires manual signing of certificate requests

    # In puppet.conf under [master] section:
    autosign = false

  On the Puppet Master (as unprivileged user) runs a service that must be reached by every node (port 8140 TCP)

  On the Client Puppet runs a root but does not expose a public service

  Sensitive data might be present in the catalog and in reports

  Sensitive data might be present in the puppet code (Propagated under a SCM)

  [Security advisories](http://www.puppetlas.com/security)
