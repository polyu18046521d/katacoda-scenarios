The microservices will generate logs to record the events happened in the service (HTTP requests). The logs generated as *.log in json format.

The logs will be collected by the Centralized Logging Service which is implemented with EFK (Elasticsearch, Filebeat, Kibana)

To make the logs useful in distributed tracing, a `trace_id` and `span_id` is added in the logs.

The idea of the `trace_id` and `span_id` is implemented with redis. It is important to make the service be stateless. We cannot use a variable to maintain and keep track of the `trace_id` and `span_id`.

The `trace_id` represents a series of events to format a meaningful action. The `span_id` represents the event_id in that microservice.

The `trace_id` is passed to other microservices by HTTP Request header. We added a new custom header Trace-Id to store the `trace_id` value. Each Microservice will check if the request header contain the `trace_id` and will create a new `trace_id` if it does not.

You can see the sample of logs by:

`cat ./logging/menu-read-service.log`{{execute T1}}