# Micro-Services

## Types of services:
* RPC are persistent services that process a request and return a response
* Consumers are also persistent services that process events from a stream
* Jobs are started when required to perform a function then terminate when finished

Consumers are asynchronous services because the caller does not wait for a response. They are preferred over RPC services, although in many cases the caller does want an answer and requires an RPC service. As a simple rule, your change requests (create, delete, update) should be asynchronous, while get requests are synchronous.

## Components
Micro-Services uses a combination of many reuasable components:
* Config changes the behavior of a service
* Data stores provide a persistent storage when the service restart and between multiple instances of the same service
* Clients to call other RPC services
* Producers to send events to Consumer services
* Stats provide real-time insight into the status of the service
* Audits provide a history of what it did

## Concepts
The following are well-known programming concepts used in the above components:
* Circuit Breakers are used in clients to detect availability of the remote service and return an error when it is not available, until it becomes available, not to flood the network with unnecessary connection/retry attempts that may cause the remote service to fail when it tries to recover.
* Gateways manages the number of connections to service. It can often handle more connections than the service itself, and may also implement authentication, authorization, throttle, transformation and other useful features.
* Callbacks (like webhooks) can be registered for the remote service to notify the caller. This means there is no open context required while the remote service completes its task. A callback may remain registered or be used only once then cancelled.
* Routers analyse a message then forward it to different end points based on a set of rules.
* Throttles limit the rate of events
* Authentication validates the identity of the caller
* Authorization is done after authentication to confirm the caller is allowed to perform the specified action.
* Transformation converts data from one form to another which is useful when the caller and the called service do not align completely. Also for handling different versions of an interface etc. It can also be used to change encoding e.g. from JSON to ASN.1
* Aggregation basically summarizes data
* Workers are (like) concurrent threads inside a service to work on multiple requests or events at the same time.
* Instances are complete services running in parallel to other similar instances.
* Schemas define the format of data, what fields it may contain and the constraints on the value of each field.
* Encoding presents data in different formats, for example the value 10 can be encoded as hexadecimal 0xa. Common data encodings today are JSON, XML and ASN.1. Inside data encoding, each value may also have an encoding, especially text may be encoded as simple ASCII text or UTF-8 etc.
