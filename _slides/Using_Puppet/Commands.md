# Using the Puppet command

Puppet has different subcommands for different purproses. It's possible to add seamlessly new commands using the **face** interface.

    puppet help

    Usage: puppet <subcommand> [options] <action> [options]

    Available subcommands: (here shown the most used ones)

    agent             The puppet agent daemon
    apply             Apply Puppet manifests locally
    ca                Local Puppet Certificate Authority management.
    cert              Manage certificates and requests
    config            Interact with Puppet's settings.
    describe          Display help about resource types
    device            Manage remote network devices
    doc               Generate Puppet references
    facts             Retrieve and store facts.
    master            The puppet master daemon
    module            Creates, installs and searches for modules on the Puppet Forge.
    node              View and manage node definitions.
    parser            Interact directly with the parser.
    resource          The resource abstraction layer shell


# Puppet operational modes

## Master / Client - puppet agent

It's the typical Puppet setup

- We have clients, our managed nodes, where Puppet agent is installed.

- We have one or more Masters where Puppet server runs as a service

- Client/Server communication is via https (**port 8140**)

- Clients certificates have to be accepted (**signed**) on the Master

- Command used on the client: ```puppet agent```  (generally as **root**)

- Command used on the server: ```puppet master```  (generally as **puppet**)


## Masterless - puppet apply

Master less mode doesn't use a client-server infrastructure.

- Our Puppet code (written in manifests) is applied directly on the target system.

- No need of a Puppet Master

- We have to distribute our modules and data to the managed nodes.

- Command used: ```puppet apply``` (generally as **root**)
