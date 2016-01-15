# Data in Modules

Hiera Data in Modules • put hiera data directly into your modules • requires future parser
28. Hiera Data in Modules /etc/hiera/hiera.yaml • needs hiera V2 conﬁguration version: 2 hierarchy: [ [ ‘osfamily’, ‘${osfamily}’, ’${osfamily}’ ], [ ‘environment’, ‘${environment}’, ‘$ {environment}’ ], [ ‘common’, ‘true’, ‘common’ ] ] backends: - yaml
29. Hiera Data in Modules <modulepath>/<modulename>/ data/ osfamily/ environment/ common.yaml manifests/ ﬁles/ hiera.yaml RedHat.yaml production.yaml
30. Hiera Data in Modules <modulepath></modulename>/ hiera.yaml • needs hiera.yaml in module —- version: 2
31. Hiera Data in Modules common.yaml ntpserver: ntp1.ptb.de ! • osfamily/Debian.yaml hiera data follow common patterns ntpserver: 10.0.2.133 ! environment/dev.yaml ntpserver: 127.0.0.1
32. Hiera Data in Modules • explizit lookups work like hiera v1 class my class ( $myvar ){ } ! hiera-data: class::myvar: ‘value’
33. Hiera Data in Modules • implizit lookups use the lookup function class my class ( $myvar = lookup(‘myvar’) ){ } ! hiera-data: myvar: ‘value’
34. Hiera Data in Modules • hiera data now use puppet variable syntax myvar: ‘Hi ${othervar}’ ! myvar2: ‘Hello ${array[2]}’ ! myvar3: ‘Hello ${lookup(akey)}’
