Python Library
==============

PythX is a Python library for the `MythX API <https://mythx.io/v1/openapi>`_.

It's goal is to facilitate development of use cases that go beyond bare API
interaction by making it easy for developers to hook into high-level
interfaces.
When writing a complex tool around MythX you shouldn't have to worry about
refreshing your JWT tokens regularly or basic consistency checking of your
requests. PythX tries to take these tedious tasks away from you - unless you
explicitly tell it not to.


Installation
------------
PythX runs on Python 3.5+.

To get started, simply run

.. code-block:: console

    $ pip3 install pythx


Example
-------

.. code-block:: python3

    from pythx import Client


    # login as free trial user
    c = Client(eth_address="0x0000000000000000000000000000000000000000", password="trial")

    # submit bytecode, source files, their AST and more!
    resp = c.analyze(bytecode="0xfe")

    # wait for the analysis to finish
    while not c.analysis_ready(resp.uuid):
        time.sleep(1)

    # have all your security report data at your fingertips
    for issue in c.report(resp.uuid):
        print(issue.swc_title or "Undefined", "-", issue.description_short)

    # Output:
    # Assert Violation - A reachable exception has been detected.
    # Undefined - MythX API trial mode.


Check out the `repository <https://github.com/dmuhs/pythx>`_, read through our
`documentation <https://pythx.readthedocs.io/en/latest/>`_, and hit us up on
`Discord <https://discord.gg/hkuxns2>`_ if you have any issues, feedback, or
just want to say hello. :)
