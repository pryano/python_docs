# Dictionary Validation

## schema vs voluptuous vs marshmallow vs jsonschema
I'm looking for a library to validate dictionaries from configuration files.
I'll need to be able to define constraints for both keys and values.
The library must support XOR key constraints.

### schema
* License: MIT
* Dictionary schemas are written in-line.
* Constraints are composed via functions.
* Supports key constraints.
* Does not support XOR constraints.

### voluptuous
* License: BSD-3
* Supports key constraints.
* Does not support XOR constraints.

### marshmallow
* License: MIT
* Does not support key constraints.
* Does not support XOR constraints.

### cerberus
* License: ISC
* Constraints are declared, not composed via chaining.
* Support XOR (oneOf).
* Supports key constraints.
