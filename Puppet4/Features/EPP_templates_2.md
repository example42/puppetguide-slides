# Epp templates

Iterations need to be specified in Puppet DSL syntax:

    # hosts hash
    $ssh_hosts = {
      'mail' => {
        'forward_x11'   => 'no',
      }
    }

    # ssh config for user
    <% $ssh_hosts.each |$host, $map| { -%>
    Host <%= $host %>
      <% if $map['forward_x11'] { -%>
      ForwardX11 <%= $map['forward_x11'] %>
      <% } -%>
    <% } -%>

