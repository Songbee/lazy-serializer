Beerializer
===========

**Deprecated:** this project haven't received the love it needs for a few
years now. I kindly suggest using `Pydantic <https://pydantic-docs.helpmanual.io/>`__
for new projects (and for backend development, check out the awesome
`FastAPI <https://fastapi.tiangolo.com/>`__ framework!).

.. image:: https://img.shields.io/badge/docs-latest-green.svg
           :target: https://beerializer.songbee.net/
           :alt: Documentation
.. image:: https://img.shields.io/pypi/v/beerializer.svg
           :target: https://pypi.org/project/beerializer/
           :alt: PyPI

A fork of awesome `R2DTO <https://github.com/nickswebsite/r2dto>`__ by
`nickswebsite <https://github.com/nickswebsite>`__.

Beerializer provides easy interface for transformation and validation of
arbitrary python objects into DTOs suitable for receiving from and delivering
to other services.

Quick Start
-----------

Let's start by creating a simple model class:

.. code:: python

    class Simpson(object):
        def __init__(self):
            self.first_name = ""
            self.last_name = ""

        def __str__(self):
            return self.first_name + " " + self.last_name

To create a serializer, we need to map attributes to fields of our DTO:

.. code:: python

    class SimpsonSerializer(Serializer):
        class Meta:
            model = Simpson

        first_name = fields.StringField(name="firstName")
        last_name = fields.StringField(name="lastName")

When you get a payload that requires one of these serializers, call
``Serializer.load(data)``.

.. code:: pycon

    >>> data = {
    ...     "firstName": "Homer",
    ...     "lastName": "Simpson",
    ... }
    >>> s = SimpsonSerializer.load(data)
    >>> s
    <class '__main__.Simpson'>
    >>> str(s)
    'Homer Simpson'

To go the other way. Pass the object you want to transfer into the
``dump`` method:

.. code:: pycon

    >>> homer = Simpson()
    >>> homer.first_name = "Homer"
    >>> homer.last_name = "Simpson"
    >>> s = SimpsonSerializer.dump(homer)
    >>> s
    {'firstName': 'Homer', 'lastName': 'Simpson'}

Ready for the journey? Install it, then check out `the docs`_::

    $ pip install -U beerializer

.. _the docs: https://beerializer.songbee.net/
