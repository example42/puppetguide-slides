
# Puppet 3 paths

**/var/log/puppet** contains logs (but also on normal syslog files, with facility daemon), both for agents and master

**/var/lib/puppet** contains Puppet operational data (catalog, certs, backup of files...)

**/var/lib/puppet/ssl** contains SSL certificate

**/var/lib/puppet/clientbucket** contains backup copies of the files changed by Puppet

**/etc/puppet/manifests/site.pp** (On Master) The first manifest that the master parses when a client connects in order to produce the configuration to apply to it (Default on Puppet < 3.6 where are used **config-file environments**)

**/etc/puppet/environments/production/manifests/site.pp** (On Master) The first manifest that the master parses when using **directory environments** (recommended from Puppet 3.6 and default on Puppt >= 4)

**/etc/puppet/modules** and **/usr/share/puppet/modules** (On Master) The default directories where modules are searched

**/etc/puppet/environments/production/modules** (On Master) An extra place where modules are looked for when using **directory environments**

# Puppet 4 paths
