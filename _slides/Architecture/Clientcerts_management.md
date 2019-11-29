# Certificates management

On the Puppet server is typically created a Certification Authority which manages all the nodes' certificates.

Starting from Puppet 6 the CA has been integrated in the puppetserver application and moved from the common puppet executable.

We are going to review here the most common commands to manage certificates in both the tools.

List the (client) certificates to sign:

    puppet cert list                            # Puppet <  6
    puppetserver ca list                        # Puppet >= 6

List all certificates: signed (+), revoked (-), to sign ( ):

    puppet cert list --all                      # Puppet <  6
    puppetserver ca list --all                  # Puppet >= 6

Sign a node's certificate:

    puppet cert sign <certname>                 # Puppet <  6
    puppetserver ca sign --certname <certname>  # Puppet >= 6

Remove a client certificate:

    puppet cert clean <certname>                # Puppet <  6
    puppetserver ca clean --certname <certname> # Puppet >= 6

To see the path of the ```ssldir``` where all certs are written:

    puppet config print ssldir

Client stores its certificates and the server's public one in ```$ssldir```.

Server stores clients public certificates and in ```$ssldir/ca```. DO NOT remove this directory.
