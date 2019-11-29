# A Catalog  of abstracted resources

The **catalog** is the complete list of resources, and their relationships, that the Puppet Master generates for the client node and sends it in Json format.

It's the result of all the puppet code and Hiera data that we define for a given node and is applied on the client after it has been received from the master.

The client uses the RAL (Resource Abstraction Layer) to execute the actual system's commands that convert abstract resources like

    @@@ puppet
    package { 'openssh': }

to their actual fulfillment on the system, such as

    @@@ shell
    apt-get install openssh # On Debian derivatives
    yum install openssh     # On RedHad derivatives

The catalog is saved by the client in:

    $libdir/client_data/catalog/$certname.json

The `$libdir` depends on the Puppet version and OS used, find it with the command `puppet config print libdir`.