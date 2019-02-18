Call
=====

Object schema
~~~~~~~~~~~~~~~~~~

- `from`: `String` - The address for the sending account. Uses the web3.eth.defaultAccount property, if not specified.
- `to`: `String` - (optional) The destination address of the message, left undefined for a contract-creation transaction.
- `blockNumber`: `Number` - the block number.
- `hash`: `String` - hash of the transaction.
- `blockHash`: `String` - hash of the block.
- `method`: `String` - name of the method that was called during the transaction.
- `probability`: `Float` - the truthness of this call. 1.0 is the best.


Call arguments
~~~~~~~~~~~~~~~

The transaction call's arguments with it's corresponding input values are located in an object representation in an array of arguments.
This allows different calls to have different types and numbers of arguments.

The argument object's structure:

- `name` - the argument's name in human readable form
- `pos` -  the index of the argument's position in the call
- `value.hex`,`value.scaled`, `value.num` - the value of the calls argument in it's corresponding representation
- `value.type` - the type of the argument's value, can be any type as specified for Solidity


Mapping
~~~~~~~

For some fields, there are multiple encodings available, which are nested as properties on the field.
More information on those data types can be found :doc:`here <../data-types/index>`.

The following is the output of the Elasticsearch mapping for the `Call` type:



.. literalinclude:: ../mappings/call.json
	:language: json
