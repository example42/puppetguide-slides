# Certificates management

On the Master we can use ```puppet cert``` to manage certificates.

List the (client) certificates to sign:

    puppet cert list

List all certificates: signed (+), revoked (-), to sign ( ):

    puppet cert list --all

Sign a client certificate:

    puppet cert sign <certname>

Remove a client certificate:

    puppet cert clean <certname>

To see the path of the ```ssldir``` where all certs are writte:

    puppet config print ssldir

Client stores its certificates and the server's public one in ```$ssldir```.

Server stores clients public certificates and in ```$ssldir/ca```. DO NOT remove this directory.
