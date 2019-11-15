# Types reference

### Online [Type Reference](http://docs.puppetlabs.com/references/latest/type.html)

This is the complete reference for Puppet types based on the latest version.

Check [here](http://docs.puppetlabs.com/references/index.html) for the reference on all the older versions.

Check the Puppet Core [Types Cheatsheet](http://docs.puppetlabs.com/puppet_core_types_cheatsheet.pdf) for an handy PDF with the essential reference.


### Inline documentation on types

We can check all the types documentation via the command line:

    @@@ shell
    puppet describe <type>

For a more compact output:

    @@@ shell
    puppet describe -s <type>

To show all the available resource types:

    @@@ shell
    puppet describe -l

### Interacting with system's types

To interactively inspect and modify our system's resources

    @@@ shell
    puppet resource <type> [name]

Remember we can use the same command to CHANGE our resources attributes:

    @@@ shell
    puppet resource <type> <name> [attribute=value] [attribute2=value2]
