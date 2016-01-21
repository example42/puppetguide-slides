
# PuppetDB API
PuppetDB exposes an [HTTP API](http://docs.puppetlabs.com/puppetdb/latest/api/) that uses a Command/Query Responsibility Separation (CQRS) pattern:

#### REST for reading
A standard REST API is used to query data.

The current (API v3) available endpoints are: ```metrics```, ```fact-names```, ```facts```, ```nodes```, ```resources```, ```reports```, ```events```, ```event-counts```, ```aggregate-event-counts```, ```server-time```


#### COMMANDS for writing
Explicit **commands** are used (via HTTP using the /commands/ URL) used to populate and modify data.

The current [**commands**](http://docs.puppetlabs.com/puppetdb/latest/api/commands.html) are: ```replace catalog```, ```replace facts```, ```deactivate node```, ```store report```.


### API versions  
There are different versions of the APIs as they evolve with PuppetDB versions.

As October 2013, Version 1 of the API is deprecated, Version 2 and 3 (the latter adds new endpoints and is recommended) are both supported.

We can access a specific version of the API using the relevant prefix:

    http[s]://puppetdb.server/v#/<endpoint>/[NAME]/[VALUE][?query=<QUERY STRING>]

### Query language
Queries to the REST endpoints can define search scope and limitations for the given endpoint. The query are sent as an "URL-encoded JSON array in prefix notation". Check the online [tutorial](http://docs.puppetlabs.com/puppetdb/latest/api/query/tutorial.html) for details.
