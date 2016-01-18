# Puppet Server

The big difference is within Ruby gems. On the old Puppet master one could make use of any Ruby gem.
Now the Puppet server is running on top of JRuby.
JRuby does not support gems with native extensions (extensions which get compiled during installation).

Please carefully review the [list](https://github.com/jruby/jruby/wiki/C-Extension-Alternatives) of gems with JRuby support.

Gems which are required for functions or report processors (not providers or facter extensions) have to be installed within the puppet server JRuby installation.
This can be done be running the ```puppetserver gem``` command:

    puppetserver gem list
    sudo puppetserver gem install rake --no-ri --no-rdoc


