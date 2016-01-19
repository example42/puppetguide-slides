# Epp templates

EPP templates can make use of parameters.
This is helpful when specifying a generic tempate which is used by several modules.

Declaration of parameters is part of the epp function and specified within a hash:

    content = epp('<path to template>', {
      'header'       => 'Copyright example42',
      'informations' => ['Puppet 4', 'EPP']
    }),

Parameters need to be specified as a header:

    <%- | String $header = '',
          Array  $informations = [] | -%>
    <%= $header %>
    List of informations:
    <% $informations.each | String $info | { -%>
      - <%= $info %>
    <% } -%>


