# Anatomy of a Puppet Run - Part 1: Catalog compilation

Execute Puppet on the client

Client shell # puppet agent -t

If pluginsync = true (default from Puppet 3.0) the client retrieves all extra plugins (facts, types and providers) present in modules on the server's $modulepath

Client output # Info: Retrieving plugin

The client runs facter and send its facts to the server

Client output # Info: Loading facts in /var/lib/puppet/lib/facter/... [...]

The server looks for the client's hostname (or certname, if different from the hostname) and looks into its nodes list

The server compiles the catalog for the client using also client's facts

Server's logs # Compiled catalog for <client> in environment production in 8.22 seconds

If there are not syntax errors in the processed Puppet code, the server sends the catalog to the client, in PSON format.

# Anatomy of a Puppet Run - Part 2: Catalog application

Client output # Info: Caching catalog for <client>

The client receives the catalog and starts to apply it locally
If there are dependency loops the catalog can't be applied and the whole tun fails.

Client output # Info: Applying configuration version '1355353107'

All changes to the system are shown here. If there are errors (in red or pink, according to Puppet versions) they are relevant to specific resources but do not block the application of the other resources (unless they depend on the failed ones).

At the end ot the Puppet run the client sends to the server a report of what has been changed

Client output # Finished catalog run in 13.78 seconds

The server eventually sends the report to a Report Collector
