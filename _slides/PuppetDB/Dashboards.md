
# PuppetDB console and tools

#### Integrated console: Anaylize PuppetDB performance
PuppetDB provides a performances dashboard out of the box, we can use it to check how the software is working: **http://<puppetdb.server>:8080/dashboard/**.
This is integral part of the PuppetDB software.

#### Puppet Board: Query PuppetDB from the web
A nice frontend that allows interrogation of the PuppetDB from the web is [PuppetBoard](https://github.com/nedap/puppetboard).
This software is contributed from the community.

#### Puppetdbquery module: Query PuppetDB from Puppet manifests
An incredibly useful module that provides faces, functions and hiera backends that work with PuppetDB is the [puppetdbquery module](https://github.com/dalen/puppet-puppetdbquery). We can install it also from the Forge:

      puppet module install dalen-puppetdbquery

This software is contributed from the community (and is becoming a standard de facto for PuppetDB querying inside Puppet modules).
