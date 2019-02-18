Contract
========

Object schema
~~~~~~~~~~~~~~~~~~

- `address`: `String`- address of the deployed contract.
- `abi`: `String` - the application binary interface of the deployed contract, formatted in JSON.
- `probability`: `Float` - the truthness of this contract information. 1.0 is the best.


Mapping
~~~~~~~

For some fields, there are multiple encodings available, which are nested as properties on the field.
More information on those data types can be found :doc:`here <../data-types/index>`.

The following is the output of the Elasticsearch mapping for the `Contract` type:



.. literalinclude:: ../mappings/contract.json
	:language: json
