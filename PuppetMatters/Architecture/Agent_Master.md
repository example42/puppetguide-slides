# Agent / Setup

  A Puppet server (running as 'puppet') listening on 8140 on the Puppet Master (the server )

  A Puppet client (running as 'root') on each managed node

  Client can be run as a service (default), via cron (with random delays), manually or via MCollective

  Client and Server have to share SSL certificates. New client certificates must be signed by the Master CA

  It's possible to enable automatic clients certificates signing on the Master (be aware of security concerns)
