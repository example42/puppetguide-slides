# Using the Puppet command

Puppet has different subcommands for different purposes. It's possible to add seamlessly new commands using the **face** interface. Here's a sample output from Puppet 6, other versions might have slightly different subcommands, but the most important ones have been there since early times.

    Usage: puppet <subcommand> [options] <action> [options]

    Available subcommands:

    Common:
        agent             The puppet agent daemon
        apply             Apply Puppet manifests locally
        config            Interact with Puppet's settings.
        help              Display Puppet help.
        lookup            Interactive Hiera lookup
        module            Creates, installs and searches for modules on the Puppet Forge.
        resource          The resource abstraction layer shell


    Specialized:
        catalog           Compile, save, view, and convert catalogs.
        describe          Display help about resource types
        device            Manage remote network devices
        doc               Generate Puppet references
        epp               Interact directly with the EPP template parser/renderer.
        facts             Retrieve and store facts.
        filebucket        Store and retrieve files in a filebucket
        generate          Generates Puppet code from Ruby definitions.
        node              View and manage node definitions.
        parser            Interact directly with the parser.
        plugin            Interact with the Puppet plugin system.
        script            Run a puppet manifests as a script without compiling a catalog
        ssl               Manage SSL keys and certificates for puppet SSL clients
        strings           Generate Puppet documentation with YARD.

# Puppet operational modes

## Master / Client - puppet agent

It's the typical Puppet setup

- We have clients, our managed nodes, where Puppet agent is installed.

- We have one or more Masters where Puppet server runs as a service

- Client/Server communication is via https (**port 8140**)

- Clients certificates have to be accepted (**signed**) on the Master

- Command used on the client: ```puppet agent```  (generally as **root**)

- Command used on the server:

  - Legacy Ruy based master in old Puppet versions: ```puppet master```  (generally as **puppet**)
  - "New" separated PuppetServer Clojure application `puppetserver`

## Masterless - puppet apply

Master less mode doesn't use a client-server infrastructure.

- Our Puppet code (written in manifests) is applied directly on the target system.

- No need of a Puppet Master

- We have to distribute our modules and data to the managed nodes.

- Command used: ```puppet apply``` (generally as **root**)

## Agentless mode

It's possible to apply Puppet manifests on a node where Puppet is not installed using **bolt**.

The command `bolt apply <manifest>` will act on a remote node, accessible via ssh or winrm, and apply there the local manifest containing Puppet code.

No Puppet package is needed on the remote node (bolt will install it under the hoods) and no service is needed.
