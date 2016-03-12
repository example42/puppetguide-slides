# Nodes classification

We can classify nodes, that is define for each of them what classes and parameters to include, in different ways:

- Using the node statement
- Using an External Node Classifier
- Using Hiera

## Classification via node statement

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

A node can inherit another node and include all the classes and variables defined for it, this feature (nodes inheritance) is now deprecated and is not supported anymore on Puppet 4.


## Nodes classification via an ENC

Puppet can query an external source to retrieve the classes and the parameters to assign to a node. This source is called External Node Classifier (ENC) and can be anything that, when interrogated via a script with the clients' certname as first parameter, returns a yaml file with the list of classes and parameters.

Common ENC are **Puppet DashBoard**, **The Foreman** and **Puppet Enterprise** (where the functionality of ENC is enabled by default).

To enable the usage of an ENC set these parameters in ```puppet.conf```

    # Enable the usage of a script to classify nodes
    node_terminus = exec

    # Path of the script to execute to classify nodes
    external_nodes = /etc/puppet/node.rb

## Classification with Hiera

Hiera provides a **hiera_include** function that allows the inclusion of classes as defined on Hiera. This is an approach that can be useful when there's massive usage of Hiera as backend for Puppet data.

In the manifest file just write:

    hiera_include('classes')

and place, as an array, the classes to include in our Hiera data source under the key ```classes```.


## Nodeless setup

It's possible also to skip the nodes classification and define what to provide on each node just using (top scope or facts) variables.

For example we may define the ```$::role``` of our systems via a fact or a variable defined according to the hostname of our clients and just include, for each of them the relevant role class:

    include "::roles::${::role}"
