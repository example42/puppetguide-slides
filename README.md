# The [DevOps] Guide to Puppet, Universe, and Everything

This is an holistic documentation project about Puppet.

It consists on:

- An Open Source [book](https://github.com/example42/puppetguide-book)

- A set of sample Puppet code [architectures](https://github.com/example42/puppetguide-architectures)

- A modular set of [Slides](https://github.com/example42/puppetguide-slides) (this repo)

- The [Puppet Universal Reference](https://github.com/example42/puppetguide-reference)

To support this project check our [IndieGogo campaign](https://www.indiegogo.com/campaigns/the-devops-guide-to-puppet-universe-and)

## Slides

Slides are in markdown format and are rendered using Puppet Labs's [showoff](https://github.com/puppetlabs/showoff).

We have different slides deck, for different purposes and skills:

- Beginner (Puppet usage and language basics)
- Intermediate (Deeper into Puppet language and components)
- Advanced (Design of Puppet infrastructures, extensions development)
- Alien (Puppet to manage Windows, Cloud infrastructures and network devices)

You can find the source markdown files under the relevant directories.

In order to show them you have to install showoff:

    gem install showoff

Then cd to the section you want to present and run showoff:

    cd Beginner
    showoff serve

Browse to http://127.0.0.1:9090 to see the slides.

Type ```t``` to show the table of contents.
