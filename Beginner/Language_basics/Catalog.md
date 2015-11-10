# The Catalog

The **catalog** is the complete list of resources, and their relationships, that the Puppet Master generates for the client and sends it in Json format.

It's the result of all the puppet code and logic that we define for a given node in our manifests and is applied on the client after it has been received from the master.

The client uses the RAL (Resource Abstraction Layer) to execute the actual system's commands that convert abstract resources like

    package { 'openssh': }

to their actual fulfillment on the system, such as

    apt-get install openssh # On Debian derivatives
    yum install openssh     # On RedHat derivatives


The catalog is saved by the client in:

    $libdir/client_data/catalog/$certname.json
