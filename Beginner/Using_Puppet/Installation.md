# Open Source Puppet Puppet installation

Puppet can be found by default in most distributions.

It generally recommended to use [Puppet Labs repositories](http://docs.puppetlabs.com/guides/puppetlabs_package_repositories.html) for the latest updates.

Check the [Installation Instructions](http://docs.puppetlabs.com/guides/installation.html) for different OS.

## Puppet 3.x installation

On Debian and derivates, you can install it with:

    apt-get install puppet       # On clients (nodes)
    apt-get install puppetmaster # On server (master)

On RedHat and derivates you need to add the EPEL repository or RHN Extra channel:

    yum install puppet        # On clients (nodes)
    yum install puppet-server # On server (master)



## Puppet 4 installation

Puppet version 4 can be installed using [Puppet Labs Software Collections](https://puppetlabs.com/blog/welcome-puppet-collections), once added the relevant repositories for your distro you can install it with:

    [apt-get|yum] install puppet-agent   # On clients (nodes)
    [apt-get|yum] install puppet-server  # On server (master)


# Puppet Enterprise installation

For complete installation instruction check the [Official Documentation](https://docs.puppetlabs.com/pe/latest/install_basic.html)

Puppet Enterprise is licenced software, you can request an trial version from [the Download page](https://puppetlabs.com/download-puppet-enterprise), it's free up to 10 managed nodes


## Puppet Enterprise Server setup

- Get the tar from [the Download page](https://puppetlabs.com/download-puppet-enterprise)

- Unpack and run:

    tar -xf <tarball>
    cd <tarballdir>
    sudo ./puppet-enterprise-installer

- Via browser open ```https://<server_name>:3000``` and follow up with web based installation (don't close your installer terminal window)

- Choose between **all in one** installation or split installation, set the puppet server certname and aliases, set the console admin password and other installation options

- Once installed, open the **Puppet Enterprise Console** via browser at ```https://server_name>```, with user **admin** and the password set before


## Puppet Enterprise agent setup

Check the official [install client documentation](http://docs.puppetlabs.com/pe/latest/install_agents.html) for complete reference.

Different alternatives:

- Run the remote installation script:

        curl -k https://<puppet_server>:8140/packages/current/install.bash | sudo bash

- Distribute the tarball and eventually use an answer file for unattended setup:

        sudo ./puppet-enterprise-installer -a ~/pe_answers.txt

- Use dedicated public modules
