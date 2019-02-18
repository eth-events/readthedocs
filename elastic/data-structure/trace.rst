Trace
===========

Object schema
~~~~~~~~~~~~~
The `trace` object inherits it's properties from the parity replay transaction object, as specified in the `parity API <https://wiki.parity.io/JSONRPC-trace-module#trace_replaytransaction>`__:

Mapping
~~~~~~~

For some fields, there are multiple encodings available, which are nested as properties on the field.
More information on those data types can be found :doc:`here <../data-types/index>`.

The following is the output of the Elasticsearch mapping for the `Trace` type:


.. literalinclude:: ../mappings/trace.json
	:language: json
