# Epp templates

In Puppet 4 we can use EPP templates instead of the usual (and still valid) erb templates.

EPP templates are evaluated via the  ```epp``` function.

EPP templates contain text and puppet DSL code. This is the major difference to ERB templates, which contain text and ERB (embedded ruby) code.

Examples:

    # sshd config
    Port <%= $port %>
    ListenAddress <%= $facts['networking']['interfaces']['eth1']['bindings']['address'] %>
    PermitRootLogin <%= $root_login %>
    ...

