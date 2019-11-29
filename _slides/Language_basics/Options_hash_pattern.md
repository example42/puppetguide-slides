# Modules reusability patterns: Template + Options hash

Check this [blog post](http://www.example42.com/2014/10/29/reusability-features-every-module-should-have/) for details.

Classes and defines should expose parameters that allow to override the used templates and set a custom hash of configurations.

    @@@puppet
    class redis (
      $config_file_template = 'redis/redis.conf.erb',
      $options_hash         = {},
    ) {
      file { '/etc/redis/redis.conf':
        content => template($config_file_template),
      }
    }


# Template + Options hash example:

Given the previous class definition, we can configure it with this sample Hiera data, in YAML format:

    @@@puppet
    ---
    redis::config_file_template: 'site/redis/redis.conf.erb'
    redis::options_hash:
      port: '12312'
      bind: '0.0.0.0'
      masterip: '10.0.42.50'
      masterport: '12350'
      slave: true

The referenced template stays in our site module, in ```$modulepath/site/templates/redis/redis.conf.erb``` and may look like:

    port <%= @options_hash['port'] %>
    bind <%= @options_hash['bind'] %>
    <% if @options_hash['slave'] == true -%>
    slaveof <%= @options_hash['masterip'] %> <%= @options_hash['masterport'] %>
    <% end -%>
