# A typical Agent / Master Setup

A typical modern Puppet infrastructure has the following components:

- a **Puppet server** service (running as user ```puppet```) listening on TCP port 8140 on the Puppet Master node (the server). This service can be supplied by different softwares:

  - The normal Puppet software in Ruby, running with the **master** command (this is usually invoked via **Passenger**, in not small setups)

  - The new **puppetserver** Clojure application, which runs inside a JVM

-  a **Puppet client** (running as ```root```) on each managed node. This is provided by the **puppet** package (for Puppet 4, when provided via the PuppetLabs repositories, this is called **puppet-agent**).

- an optional **PuppetDB** service, which need to communicate with the Puppet server and uses **PostgreSQL** as data backend.

- an optional **MCollective** infrastructure based on agents, running on each node, a console, used from an administrative node for centralized control, and a Message Queue middleware service (typically **ActiveMQ** or **RabbitMQ**)

A Puppet run on the client can be triggered in different ways:

  - As a service (default configuration), which polls the server every 30 minutes (default)

  - Via a cron job (typically with random delays to avoid requests congestion)

  - Manually from the client node

  - In a centralized way via MCollective

  - From the Puppet Master, via the [Application Orchestration](https://docs.puppetlabs.com/pe/latest/app_orchestration_overview.html) feature introduced in Puppet Enterprise 2015.3
