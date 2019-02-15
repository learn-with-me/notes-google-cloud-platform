# Cloud Pub/Sub

Simple, global, reliable real-time messaging and streaming ingestion service on the GCP. Publishers publish messages on a topic, Subscribers have subscriptions to a topic to receive the message. Subscription can be defined as a queue \(message stream\) to a subscriber, that stores messages reliably between a subscriber and pub/sub.

There can be multiple subscribers per subscription, and atleast one of the subscriber needs to acknowledge a message to pub/sub, which is enough for pub/sub to go ahead and delete the message. Which means it is NOT required for every subscriber on a subscription is actually going to receive every message. 

A topic can have multiple publishers. In addition, a publisher app can publish to multiple topics. There is a many-to-many relationship between publishers and topics. Subscribers are going to receive messages from subscriptions. Multiple subscribers can subscribe to the same subscription.

##### Features

* Many-to-many asynchronous messaging
* Decouples senders and receivers
* Reliable, scalable, secure
* At-least-once delivery
* Exactly-once processing \(in Dataflow\)
* Serverless
* Auto-scaling along all axes
  * Senders
  * Receivers
  * Number and size of messages
* Replicated

##### Messages

* Pub/Sub providers
  * At-least-once delivery
  * no guaranteed ordering
* Dataflow with Pub/Sub
  * Ordering
  * De-duplication
* You can replay acknowledged messages, provided we have retain acknowledged messages enabled

##### Topics

* Named resource to which publishers send messages
* Used to organize messages
* Publishers send messages to topics
* Subscribers subscribe to topics using subscriptions

##### Subscription

* Pub/Sub sends each message on a topic to each subscription individually
* Messages persist inside Pub/Sub
* Not deleted until at least one subscriber per subscription has acknowledged
* Each subscription then might
  * Either push messages to subscriber endpoint
    * Any app that can make HTTPS request to googleapis.com
  * Or wait for subscriber to pull them at a later point
    * Webhook endpoints that can accept HTTPS POST requests

##### Common Publishers

* Cloud Logs
* Cloud API
* Cloud Dataflow
* Cloud Storage
* Cloud functions

##### Common Subscribers

* Cloud Networking
* Compute Engine/GKE
* Cloud Dataflow
* App Engine
* Cloud Monitoring
* Cloud functions
* App on third party network, Mobile apps
* Any application that can make HTTPS request to googleapis.com







