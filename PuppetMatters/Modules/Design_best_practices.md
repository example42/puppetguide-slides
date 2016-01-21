# Principes behind a Reusable Module

Data Separation

  - Configuration data is defined outside the module
  - Module behavior can be managed via parameters
  - Allow module's extension and override via external data

Reusability

  - Support different OS. Easily allow new additions.
  - Customize behavior without changing module code
  - Do not force author idea on how configurations should be provided

Standardization

  - Follow PuppetLabs style guidelines (puppet-lint)
  - Have coherent, predictable and intuitive interfaces
  - Provide contextual documentation (puppet-doc)

Interoperability

  - Limit cross-module dependencies
  - Allow easy modules cherry picking
  - Be self contained, do not interfere with other modules' resources
