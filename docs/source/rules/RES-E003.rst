[RES-E003] - Added Enum value in Response contract
==================================================

Rationale
---------
Adding an enum value to a response parameter is backward incompatible as clients, using the "old" version of the
Swagger specs, will not be able to properly validate the response.

Mitigation
----------
A possible mitigation consists of modifying the endpoint to get the list of enum values supported for the specific request.
This way we can ensure (at the business logic level, not on Swagger) that the response will not contain enum values that
are not manageable by clients using "old" Swagger spec version.

Example
-------
Old Swagger Specs
~~~~~~~~~~~~~~~~~

.. literalinclude:: examples/RES-E003/old.yaml
   :name: Old Swagger Spec
   :language: yaml
   :linenos:

New Swagger Specs
~~~~~~~~~~~~~~~~~

.. literalinclude:: examples/RES-E003/new.yaml
   :name: New Swagger Spec
   :language: yaml
   :emphasize-lines: 17
   :linenos:


Backward Incompatibility
~~~~~~~~~~~~~~~~~~~~~~~~
The following snippet triggers the incompatibility error.

.. literalinclude:: examples/RES-E003/tester.py
   :language: py
   :linenos:

**NOTE**: The code is taking advantage of `bravado <https://github.com/Yelp/bravado>`_
