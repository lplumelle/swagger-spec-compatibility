[RES-E002] - Remove a required property from an object used in responses
========================================================================

Rationale
---------
Removing a required property from an object leads to false expectation on the client receiving the object.
If the client is using "old" service's Swagger spec it will expect the property to be presentand so it could throw errors.
It could be valid to assume that the client won't perform response validation and this leads to unexpected errors
while parsing the response and/or using the missing property.

Mitigation
----------
A known mitigation to this issue consists of keeping the required property in the Swagger specs and ensuring that
the service populate the field with a placeholder (that has to be valid with the property spec).

Example
-------
Old Swagger Specs
~~~~~~~~~~~~~~~~~

.. literalinclude:: examples/RES-E002/old.yaml
   :name: Old Swagger Spec
   :language: yaml
   :emphasize-lines: 15-16
   :linenos:

New Swagger Specs
~~~~~~~~~~~~~~~~~

.. literalinclude:: examples/RES-E002/new.yaml
   :name: New Swagger Spec
   :language: yaml
   :linenos:


Backward Incompatibility
~~~~~~~~~~~~~~~~~~~~~~~~
The following snippet triggers the incompatibility error.

.. literalinclude:: examples/RES-E002/tester.py
   :language: py
   :linenos:

**NOTE**: The code is taking advantage of `bravado <https://github.com/Yelp/bravado>`_
