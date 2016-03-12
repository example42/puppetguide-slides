# Information available on the agent

To see the list of classes included in the local node (**$classfile**):

    sudo cat /var/lib/puppet/state/classes.txt # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/state/classes.txt # Puppet 4

To see all the resources managed on the node (**$resourcefile**):

    sudo cat /var/lib/puppet/state/resources.txt # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/state/resources.txt # Puppet 4

To check the summary of the last puppet run (with metrics on performances and resources changed, **$lastrunfile**):

    sudo cat /var/lib/puppet/state/last_run_summary.yaml # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/state/last_run_summary.yaml # Puppet 4

To check the full report of the last run (not easy to read output):

    sudo cat /var/lib/puppet/state/last_run_report.yaml # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/state/last_run_report.yaml # Puppet 4

To see, in JSON pretty format, the whole content of the last saved catalog:

    sudo cat /var/lib/puppet/client_data/catalog/<node_certname>.json | json_pp # Puppet 3
    sudo cat /opt/puppetlabs/puppet/cache/client_data/catalog/<node_certname>.json | json_pp # Puppet 4

To see the Puppet agent logs:

    sudo cat /var/log/puppet/agent.log # Puppet 3
    sudo cat /var/log/puppetlabs/puppet/puppetd.log # Puppet 4
