# Deployment Manager

Simply Infrastructure-as-a-code. Similar to AWS Cloudformation

#### Broken down into:

* Configuration
  * YAML files
  * List of resources and their specifications
* Template
  * Individual parts of the configuration files separated out in their own files
  * Can be reused by multiple configurations
  * Can be written in Python or **Jinja2**
* Resource
  * Single resource defined inside a configuration. Each resource is a single element with types \(google managed type or composite type\).
  * Made up of name, type, properties
* Type
  * Base Type
  * Composite Type
* Manifest
  * Internal to deployment manager. Each deployment update creates a new read-only manifest
  * Includes imported templates and fully expanded configuration
* Deployment
  * Set of resources that are deployed and managed together
  * Can be deleted or updated. Deletion of deployment deletes corresponding resources automatically.

#### APIs to be enabled

* Deployment manager
* Compute engine API \(if working with compute engine\)



