# Variables

In our code we can define our **variables** and use other ones that may come from different sources:

- **facts** generated directly by the client
- **parameters** obtained from node's classification
- Puppet **internal** variables

### Facts

**Facter** runs on clients and collects **facts** that the server can use as variables

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


### User Variables

We can define custom variables in our Puppet code:

    $role = 'mail'

    $package = $::operatingsystem ? {
      /(?i:Ubuntu|Debian|Mint)/ => 'apache2',
      default                   => 'httpd',
    }
