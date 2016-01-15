# Developing Puppet extensions - Overview

### Developing custom facts

### Developing custom types and provides

### Developing functions



# Developing Facts

  Facts are generated on the client before the evaluation of the Puppet code on the server.

  Facts provide variables that can be used in Puppet code and templates.

  A simple custom type that just executes a shell command:

    require 'facter'
    Facter.add("last_run") do
      setcode do
        Facter::Util::Resolution.exec('date')
      end
    end

  This file should be placed in <modulename>/lib/facter/acpi_available.rb


# Developing Types

  Resource types can be defined in Puppet language or in Ruby as plugins.

  Ruby types require one or more **providers** which manage low-lovel interaction with the underlining OS to provide the more abstact resource defined in Types.

  An example of a type with many providers is package, which has more than 20 providers that manage packages on different OS.

  A sample type structure (A type called vcsrepo, must have a path like **<module_name>/lib/puppet/type/vcsrepo.rb**

    require 'pathname'

    Puppet::Type.newtype(:vcsrepo) do
      desc "A local version control repository"

      feature :gzip_compression,
              "The provider supports explicit GZip compression levels"

      [...] List of the features

      ensurable do

        newvalue :present do
          provider.create
        end

      [...] List of the accepted values

      newparam(:source) do
        desc "The source URI for the repository"
      end

      [...] List of the accepted parameters

    end


# Developing Providers

  The vcsrepo type seen before has 5 different providers for different source control tools.

  Here is, as an example, the git provider for the vcsrepo type (Code (C) by PuppetLabs):
  This file should be placed **<module_name>/lib/puppet/provider/vcsrepo/git.rb**

    require File.join(File.dirname(__FILE__), '..', 'vcsrepo')

    Puppet::Type.type(:vcsrepo).provide(:git, :parent => Puppet::Provider::Vcsrepo) do
      desc "Supports Git repositories"

      commands :git => 'git'
      defaultfor :git => :exists
      has_features :bare_repositories, :reference_tracking

      def create
        if !@resource.value(:source)
          init_repository(@resource.value(:path))
        else
          clone_repository(@resource.value(:source), @resource.value(:path))
          if @resource.value(:revision)
            if @resource.value(:ensure) == :bare
              notice "Ignoring revision for bare repository"
            else
              checkout_branch_or_reset
            end
          end
          if @resource.value(:ensure) != :bare
            update_submodules
          end
        end
      end

      def destroy
        FileUtils.rm_rf(@resource.value(:path))
      end

      [...]

    end


# Developing Functions

  Functions are Ruby code that is executed during compilation on the Puppet Master.

  They are used to interface with external tools, provide debugging or interpolate strings.

  Importants parts of the Puppet language like include and template are implemented as functions.

    module Puppet::Parser::Functions
      newfunction(:get_magicvar, :type => :rvalue, :doc => <<-EOS
    This returns the value of the input variable. For example if you input role
    it returns the value of $role'.
        EOS
      ) do |arguments|

        raise(Puppet::ParseError, "get_magicvar(): Wrong number of arguments " +
          "given (#{arguments.size} for 1)") if arguments.size < 1

        my_var = arguments[0]
        result = lookupvar("#{my_var}")
        result = 'all' if ( result == :undefined || result == '' )
        return result
      end
    end

  This file is placed in puppi/lib/puppet/parser/functions/get_magicvar.rb.
# Puppet reporting - Overview

### Reporting overview

### Understanding puppet run output


# Reporting

  In reports Puppet stores information of what has changed on the system after a Puppet run

  Reports are sent from the client to the Master, if report is enabled

    # On client's puppet.conf [agent]
    report = true

  On the Master different report processors may be enabled

    # On server's puppet.conf [master]
    reports = log,tagmail,store,https
    reporturl = http://localhost:3000/reports

# Understanding Puppet runs output

  Puppet is very informative about what it does on the functions

    /Stage[main]/Example42::CommonSetup/File[/etc/motd]/content:
    --- /etc/motd	2012-12-13 10:37:29.000000000 +0100
    +++ /tmp/puppet-file20121213-19295-qe4wv2-0	2012-12-13 10:38:19.000000000 +0100
    @@ -4,4 +4,4 @@
    -Last Puppet Run: Thu Dec 13 10:36:58 CET 2012
    +Last Puppet Run: Thu Dec 13 10:38:00 CET 2012
    Info: /Stage[main]/Example42::CommonSetup/File[/etc/motd]: Filebucketed /etc/motd to main with sum 623bcd5f8785251e2cd00a88438d6d08
    /Stage[main]/Example42::CommonSetup/File[/etc/motd]/content: content changed '{md5}623bcd5f8785251e2cd00a88438d6d08' to '{md5}91855575e2252c38ce01efedf1f48cd3'

  The above lines refer to a change made by Puppet on /etc/motd
  The File[/etc/motd] resource is defined in the class example42::commonsetup
  A diff is shown of what has changed (the diff appears when running puppet agent -t in interactive mode)
  The original file has been filebucketed (saved) with checksum 623bcd5f8785251e2cd00a88438d6d08
  We can retrieve the original file in /var/lib/puppet/clientbucket/6/2/3/b/c/d/5/f/623bcd5f8785251e2cd00a88438d6d08/contents
  We can search for all the old versions of /etc/motd with

    grep -R '/etc/motd' /var/lib/puppet/clientbucket/*
