# Variables

Variables is Puppet codes are basically **constants**: once defined in a class we can't change them.

We can set variables in our Puppet code with this syntax:

    @@@ puppet
    # Normal variable assignment
    $role = 'mail'

    # The value of a variable is based on another variable (here used the **selector** costruct)
    $package = $::operatingsystem ? {
      /(?i:Ubuntu|Debian|Mint)/ => 'apache2',
      default                   => 'httpd',
    }

Puppet automatically provides also some **internal** variables, the most common are:

- The name of the node (the certname setting in its puppet.conf)

        $clientcert # Default is the client's Fully Qualified Domain Name)

- The Puppet's environment where the Master looks for the code to compile

        $environment # Default is "production"

- The Master's FQDN and IP address

        $servername $serverip

-  Any configuration setting of the Puppet Master's puppet.conf

        $settings::<setting_name>:

-  The name of the module that contains the current resource's definition

        $module_name

# Facter and facts

**Facter** is a tools shipped with Puppet. It runs on clients and collects **facts** which are sent to the server. In our code we can use facts to manage resources in different ways or with different arguments.


Here follows a list of the most common and useful facts:

    al$ facter

    architecture => x86_64
    fqdn => Macante.example42.com
    hostname => Macante
    ipaddress_eth0 => 10.42.42.98
    macaddress_eth0 => 20:c9:d0:44:61:57
    operatingsystem => Centos
    operatingsystemrelease => 6.3
    osfamily => RedHat
    virtual => physical

It's easy to create custom facts. They can be of 2 types:

- **Native facts** written in ruby and shipped with modules (in the ```lib/facter``` directory)
- **External facts** can be simple ini-file like texts (with ```.txt``` extension), Yaml files or even commands in any language, which returns a fact name and its value. External faccts are located in the nodes' ```/etc/facter/facts.d``` directory and can be shipped also from modules (in the ```facts.d``` directory)


