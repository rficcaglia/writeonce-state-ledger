# writeonce-state-ledger
How to implement a multi-cloud compatible write only state ledger that can be used for forensics, analysis, remediation, financial analysis, etc.

Use Cases:

* tracing all events on a cloud/cluster/app into a write-once ledger that doesn't require blockchain decentralized ledger but is immutable.
* the source of the events should be tamper proof, or tamper evident.  
* use this tracing for network (micro)segmentation policy [[0]](https://pdfs.semanticscholar.org/3f15/0216fb6772a0f5a5339b693d5140122a53c5.pdf):

> In order to (achieve network segmentation), a combination of host and container-level
> traceability (is) required...(Something that) synchronizes with the Kubernetes Master through 
> heartbeat requests in order to push new states to dependent systems and provide translation between pod IP and 
> application. Logging of pod-to-pod communications based on pod-IPs as packet source and destination 
> introduce the issue of cluster state changes. Any translation between pod-IP and
> application may become invalid if the cluster state has changed. If a pod is relocated its
> pod-IP in the current state may not refer to the same application as in the previous state.
> Any log entry made in the previous state cannot be used to understand the traffic as its
> corresponding state no longer exists. To tackle this issue ... the following ... functionalities (are needed):
>    * State-mapping: Given a point in time the system can retrieve the state of the cluster during that time.
>    * Pod-mapping: Given a pod-IP and a cluster state the system can retrieve the pod corresponding to the pod-IP of that state together with information related to the pod.
>    * State-subscription: Following the publish-subscribe architectural pattern the system allows other systems to subscribe to state changes which are pushed, or published.

Brainstorm:

* use Jaeger/[OpenTracing](https://opentracing.io/) but with a plugin for storage that sends to write-once, immutable storage...see  https://github.com/jaegertracing/jaeger/pull/1461 but how can we trust the apps to provide valid and complete data?
* use https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/ but how can we prevent bad containers from faking or omitting events?
* can query API Server but then how do you prevent compromised api-server from faking or omitting events?
* can use k8s audit logging but how to prevent compromised api-server?
