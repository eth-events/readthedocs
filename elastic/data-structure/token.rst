Token
=====

Object schema
~~~~~~~~~~~~~~~~~~

- `address`: `String`- address of the deployed contract.
- `name`: `String` - a human readable name for the contract.
- `symbol`: `String` - the currency symbol of the contract.
- `totalSupply`: `Number` - the total supply of shared value for the currency.
- `links`: `Array` - an array of weblinks with description and link.
- `probability`: `Float` - the truthness of this token information. 1.0 is the best.


Mapping
~~~~~~~

For some fields, there are multiple encodings available, which are nested as properties on the field.
More information on those data types can be found :doc:`here <../data-types/index>`.

The following is the output of the Elasticsearch mapping for the `Token` type:



.. literalinclude:: ../mappings/token.json
	:language: json
