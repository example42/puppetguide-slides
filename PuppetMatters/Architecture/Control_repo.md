# The control repo

The current recommended approach to manage our Puppet code and data is to use a so called **control-repo** which is basically the content of a Puppet environment and contains typically:

- The **environment.conf** file to configure the environment itself

- A **hieradata** directory where to place Hiera data file (typically in yaml format)

- A **manifests** directory which contains manifests outside modules (maps to the **manifests** config setting). This has typically the **site.pp** manifest with some node classification technique, top scope variables and resource defaults.

- An empty **modules** directory that contains Public modules to be installed via r10k

- A **Puppetfile** that defines the public modules to install via r10k

- A **site** directory which is added to the modulepath and contains local custom modules. In this directory you have, for example the **role** and the **profile** modules and any other custom module created for local needs

- An optional **Vagrantfile** and relevant files to have a local Vagrant environment where to test the Puppet

For a sample, check [PuppetLabs' control repository template](https://github.com/puppetlabs/control-repo).
