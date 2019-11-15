# Built-in variables

Puppet provides some useful built in variables, they can be:

#### Set by the client (agent)

```$clientcert``` - the name of the node's certificate. By default its ```$::fqdn```
```$clientversion``` - the Puppet version on the client

#### Set by the server (master)

```$environment``` (default: production) - the Puppet environment where are placed modules and manifests.
```$servername```, ```$serverip``` - the Puppet Master FQDN and IP
```$serverversion``` - the Puppet version on the server
```$settings::<name>``` - any configuration setting on the Master's ```puppet.conf```

#### Set by the server during catalog compilation

```$module_name``` - the name of the module that contains the current resource's definition
```$caller_module_name``` - the name of the module that contains the current resource's declaration
