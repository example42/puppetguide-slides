# Puppet Server

Is the new [server component](http://docs.puppetlabs.com/puppetserver/2.2/index.html) to manage Puppet agents.

It's written in Clojure and runs inside a JVM.

By default it uses 2GB of RAM.

Slower startup times, better performances.

Works also with [Puppet 3 agents]()

Runs the gems needed by our modules via Juby

    puppetserver gem list
    sudo puppetserver gem install rake --no-ri --no-rdoc
