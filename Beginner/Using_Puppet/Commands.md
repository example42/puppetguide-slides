# Using the Puppet command

# Main configuration options

To view all or a specific configuration setting:

    puppet config print all
    puppet config print modulepath



# Masterless - puppet apply

Our Puppet code (written in manifests) is applied directly on the target system.

No need of a complete client-server infrastructure.

Have to distribute manifests and modules to the managed nodes.

Command used: ```puppet apply``` (generally as **root**)

# Master / Client - puppet agent

We have clients, our managed nodes, where Puppet agent is installed.

And we have one or more Masters where Puppet server runs as a service

Client/Server communication is via https (**port 8140**)

Clients certificates have to be accepted (**signed**) on the Master

Command used on the client: ```puppet agent```  (generally as **root**)

Command used on the server: ```puppet master```  (generally as **puppet**)
