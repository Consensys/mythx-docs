.. index:: curl
.. _curl:

MythX API via Curl
==================

We have written shell scripts to demonstrate how to use to the
`MythX API <https://staging.api.mythx.io/v1/openapi/>`_ at the most
basic level using `curl <https://curl.haxx.se/download.html>`_. In
using these scripts you will see the HTTP requests that get sent along
with JSON output returned as a result of each request.

This may be useful for developers writing a programming language
interfaces to MythX, or are writing a MythX service and want the most
fine-grained control over what the API has to offer. It may be useful
also in experimenting with MythX at the API level. Note however that
some programming languages like JavaScript there is already a library
that can simplify interaction with MythX.

.. seealso::

  * `The github project <https://github.com/rocky/mythx-api-curl>`_
  * `MythX API spec <https://staging.api.mythx.io/v1/openapi/>`_
  * `armlet <sdk/armlet>`_ A Javascript Wrapper around MythX
