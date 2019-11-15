# Certificates management - Puppet First run

By default the first Puppet run on a client fails:

    client # puppet agent -t
           # "Exiting; no certificate found and waitforcert is disabled"

An optional ````--waitforcert 60``` parameter makes client wait 60 seconds before giving up.

The server has received the client's CSR which has to be manually signed:

    server # puppet cert sign <certname>

Once signed on the Master, the client can connect and receive its catalog:

    client # puppet agent -t


If we have issues with certificates (reinstalled client or other certs related problemes):

Be sure client and server times are synced

Clean up the client certificate. On the client remove it:

    client # mv /var/lib/puppet/ssl /var/lib/puppet/ssl.old

On the Master clean the old client certificate:

    server # puppet cert clean <certname>
