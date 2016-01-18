# Installation Overview

With Puppet 4 Puppetlabs ships its on required and tested Ruby Version.

The packages Ruby Installation is done in a way that it will not interfere with system Ruby iinstallations.

Besides this Puppetlabs decided to also bundle all required other components directly into one single package: the puppet-agent package
This concept called the Package Collection 1.

All package content will install into the following directories:

- /opt/puppetlabs
- /etc/puppetlabs

Packaging is done for a limited set of Distributions and Versions:

- RHEL 5,6 and 7
- Debian 6,7 and 8
- Fedora 21 and 22
- Windows Server 2012 R2, 2008 R2
- Windows Vista, 7, 8 and 8.1
- OS X 10.9, 10.10 and 10.11

On other distributions one needs to take care to comply with [system requirements](https://docs.puppetlabs.com/puppet/4.3/reference/system_requirements.html).

Upon system preparation one has to ensure that name resolution is properly set up and that the time is in sync.
(Time is critical to Puppet installations as the whole communication is based upon ssl encryption with signed certificates.)

The next step is to install the puppet agent package.

