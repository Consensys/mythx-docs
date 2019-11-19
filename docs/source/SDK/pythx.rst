.. meta::
   :description: How to use PythX, a Python library for the MythX API which provides an easy-to-use interface to the official MythX API & smart contract security tools.

.. _tools.pythx:

PythX Guide: Installation & Usage
=================================

PythX is a Python library for the MythX API.

Its goal is to facilitate development of use cases that go beyond bare API
interaction by making it easy for developers to hook into high-level
interfaces.
When writing a complex tool around MythX you shouldn't have to worry about
refreshing your JWT tokens regularly or basic consistency checking of your
requests. PythX takes these tedious tasks away from you - unless you explicitly
tell it not to.


Installation
------------
PythX runs on Python 3.5+.

To get started, simply run

.. code-block:: console

    $ pip3 install pythx

Alternatively, clone the repository and run

.. code-block:: console

    $ pip3 install .

Or directly through Python's :code:`setuptools`:

.. code-block:: console

    $ python3 setup.py install


Example
-------

PythX aims to provide an easy-to-use interface to the official MythX API.
Its goal is to turbocharge tool development and make it easy to deal with
even complex use cases.

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


The PythX CLI has now become the MythX CLI!
-------------------------------------------

Originally, the PythX CLI was a proof of concept to display to interested
developers what can be done using the library. The interest in the CLI grew
so large that a lot of developers contacted me and asked for support and
new features.

This is the PSA that **I will no longer maintain the PythX CLI**. But wait!
There's more!

Because a PoC is not exactly what you would call future-proof and maintainable
software, I have decided to do a complete revamp. It is called `mythx-cli` and
incorporates all feature requests I have gotten so far. Check it out
:ref:`here <tools.mythx-cli>` and let me know what you think!

Enjoy! :)


Check out the `repository <https://github.com/dmuhs/pythx>`_, read through our
`documentation <https://pythx.readthedocs.io/en/latest/>`_, and hit us up on
`Discord <https://discord.gg/hkuxns2>`_ if you have any issues, feedback, or
just want to say hello. :)
