# writeonly-state-ledger
How to implement a multi-cloud compatible write only state ledger that can be used for forensics, analysis, remediation, financial analysis, etc.

Use Cases:

* tracing all events on a cloud/cluster/app into a write-once ledger that doesn't require blockchain decentralized ledger but is immutable.

Misc:

* use Jaeger/OpenTracing but with a plugin for storage that sends to write-once, immutable storage...see  https://github.com/jaegertracing/jaeger/pull/1461
