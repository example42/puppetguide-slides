# Certificates management

  On the Master we can use ```puppet cert``` to manage certificates

  List the (client) certificates to sign:

    puppet cert list

  List all certificates: signed (+), revoked (-), to sign ( ):

    puppet cert list --all

  Sign a client certificate:

    puppet cert sign <certname>

  Remove a client certificate:

    puppet cert clean <certname>

  Client stores its certificates and the server's public one in ```$vardir/ssl**``` (```/var/lib/puppet/ssl``` on Puppet OpenSource)

  Server stores clients public certificates and in ```$vardir/ssl/ca``` (```/var/lib/puppet/ssl/ca```). DO NOT remove this directory.
