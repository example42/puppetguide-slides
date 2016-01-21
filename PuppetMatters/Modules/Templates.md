# Erb templates

  Files provisioned by Puppet can be Ruby ERB templates

  In a template all the Puppet variables (facts or user assigned) can be used :

    # File managed by Puppet on <%= @fqdn %>
    search <%= @domain %>

  But also more elaborated Ruby code

    <% @dns_servers.each do |ns| %>
    nameserver <%= ns %>
    <% end %>

  The computed template content is placed directly inside the catalog
  (Sourced files, instead, are retrieved from the puppetmaster during catalog application)
