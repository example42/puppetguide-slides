# Data in Modules

Hiera Data in Modules
put hiera data directly into your modules
requires future parser
Hiera Data in Modules 
/etc/hiera/hiera.yaml
needs hiera V2 configuration 
version: 2 
hierarchy: [ [ 
osfamily {osfamily}{osfamily}], [ environment ${environment}], 
[ common true common ] ] 
backends: - yaml

Hiera Data in Modules 
<modulepath>/<modulename>/
 data/
 osfamily/
 environment/
 common.yaml
 
 manifests/ 
 fileles/ 
 hiera.yaml 
 RedHat.yaml 
 production.yaml

Hiera Data in Modules 
<modulepath></modulename>/ 
 hiera.yaml -- needs hiera.yaml in module
 version: 2

Hiera Data in Modules 
  common.yaml 
  ntpserver: ntp1.ptb.de
  osfamily/Debian.yaml 
  hiera data follow common patterns 
  ntpserver: 10.0.2.133
  environment/dev.yaml 
  ntpserver: 127.0.0.1

Hiera Data in Modules
explizit lookups work like hiera v1 
class my_class ( $myvar ){ }
hiera-data: 
my_class::myvar: 'value'

Hiera Data in Modules
implizit lookups use the lookup function 
class my class ( $myvar = lookup('myvar') ){ }
hiera-data: 
myvar: value

Hiera Data in Modules
hiera data now use puppet variable syntax 
myvar:'Hi ${othervar}' 
myvar2: 'Hello ${array[2]}'
myvar3: 'Hello ${lookup(akey)}



