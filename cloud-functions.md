# Cloud Functions

This is what everyone keeps saying serverless application.

> Function timeouts in 60 seconds. If you don't end it in time, You'll be charged for the whole 60 seconds

#### Trigger Types

* HTTP Trigger
* Pub/Sub Trigger
* Storage Trigger

#### Event Object

Pub/Sub and Cloud Storage functions' trigger return the event object. Here is what the object looks like:

* eventId:String
* timestamp:String
* eventType:String
* resource:String
* data:Object - Pub/Sub
  * data:String
  * attributes:Map
  * messageId:String
  * publishTime:String
* data:Object - Cloud Storage
  * Id
  * name
  * bucket
  * timeCreated/updated/deleted
  * contentType
  * metadata
  * accessControlList
  * encryption

#### Ending the function

* HTTP functions can be ended by response.send\(\)
* Other functions are ended as soon as the callback is finished

#### LifeCycle of a function

* Trigger is executed
* Spins up an instance of the cloud function
* First call will have a cold start time, which can take around 500ms
* It can take load upto 100,000 calls per second. If thats not enough, it'll automatically create other instances of the same function and setup a load balancer on top of it. Good side is that there is no charge for the infrastructure, just its use. This auto-scaling also supports spinning up new instances in case of crashes automatically.
* If there are no calls to the function for about 60 seconds, Google spins down the instance to zero



