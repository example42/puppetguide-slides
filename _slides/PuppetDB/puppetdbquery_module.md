
# Using Puppetdbquery module

The [PuppetDbQueryModule](https://github.com/dalen/puppet-puppetdbquery) is developed by a community member, Erik Dalen, and is the most used and useful module available to work with PuppetDB: it provides command lines tools (as Puppet Faces), functions to query PuppetDB and a PuppetDB based Hiera backend.

## Query format
All the queries we can do with this module are in the format

    Type[Name]{attribute1=foo and attribute2=bar}

by default they are made on normal resources, use the @@ prefix to query exported resources.

The comparison operators are: **=**, **!=**, **>**, **<** and **~**

The expressions can be combined with **and**, **not** and **or**

# Using Puppetdbquery module

## Command line

The module introduces, as a Puppet face, the **query** command:

    puppet help query
    puppet query facts '(osfamily=RedHat and operatingsystemversion=6)'

## Functions
The functions provided by the module can be used inside manifests to populate the catalog with data retrieved on PuppetDB.

**query_nodes** takes 2 arguments: the query to use and (optional) the fact to return (by default it provides the certname). It returns an array:

    $webservers = query_nodes('osfamily=Debian and Class[Apache]')
    $webserver_ip = query_nodes('osfamily=Debian and Class[Apache]', ipaddress)


**query_facts** requires 2 arguments: the query to use to discover nodes and the list of facts to return for them. It returns a nested hash in JSON format.

    query_facts('Class[Apache]{port=443}', ['osfamily', 'ipaddress'])
