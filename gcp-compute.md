# GCP Compute

Compute section has four flavors:

* App engine Standard
* App engine Flexible
* Compute engine
* Kubernetes engine
* Cloud functions - serverless

### Compute Engine

Fully controllable including configuration, load balancing, administration & management.

Ideal for situations when:

* you need complete control over infrastructure and direct access to high-performance hardware, such as GPUs and local SSDs
* you need to make OS level changes.
* you want to move your existing application from own datacenter to the cloud without rewriting it
* you need to run a software package that can't be easily containerized or you want to use existing VM images

When looking to install an operating system, here are couple of choices:

* Public images for Linux or Windows server \(provided by Google already\)
* Private image that you can create or import \(provided by user\)
* Images from marketplace \(service providers provide pre-built images with their software pre-installed\)

Storage options to choose from:

* Standard Storage Disk \(SSD0
* Cloud Storage Bucket
* Standard Persistent Disk
* Local SSD

Machine Types to choose from:

* Standard
* high memory
* high CPU
* shared core

#### Features

* Customizable load-balancing and auto-scaling across homogeneous VMs
* Direct access to GPUs that can be used to accelerate specific workloads
* 
##### Pre-emptible Instances

Cost is much less than regular VM. Used for Fault tolerant application. However terminated after 24 hours or during maintenance with a 30 seconds notice, which is why having a `shutdown script` is a must for such systems.





