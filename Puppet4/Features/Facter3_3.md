# Facter 3

With facter 2 it was possible to get all facts plus all puppet facts by running the command ```facter -p```

This option has been removed.

To get all facter values plus Puppet facts the command ```puppet facts``` has to be run.

Facter can also be used independently from Puppet. e.g. if you want the facts to show up as json, run ```facter -j``` (which is the default).
If you prefer yaml output run ```facter -y```

