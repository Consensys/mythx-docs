.. meta::
   :description: How to use the MythX CLI Python package to provide a simple-to-use command line interface for the MythX API.

.. _tools.mythx-cli:

MythX CLI Guide: Installation & Usage
=====================================

.. note:: See the `MythX CLI documentation <https://mythx-cli.readthedocs.io>`_ for full details on usage.

The `MythX CLI <https://github.com/dmuhs/mythx-cli/>`_ Python package aims to
provide a simple to use command line interface for the MythX API. It's main
purpose is to demonstrate how advanced features can be implemented using the
`PythX <https://github.com/dmuhs/pythx/>`_ Python language bindings for MythX
to simplify API interaction.


Usage
-----

.. code-block:: console

    $ mythx
    Usage: mythx [OPTIONS] COMMAND [ARGS]...

      Your CLI for interacting with https://mythx.io/

    Options:
      --debug / --no-debug            Provide additional debug output
      --access-token TEXT             Your access token generated from the MythX
                                      dashboard
      --eth-address TEXT              Your MythX account's Ethereum address
      --password TEXT                 Your MythX account's password as set in the
                                      dashboard
      --format [simple|json|json-pretty]
                                      The format to display the results in
      --help                          Show this message and exit.

    Commands:
      analyze  Analyze the given directory or arguments with MythX.
      list     Get a list of submitted analyses.
      report   Fetch the report for a single or multiple job UUIDs.
      status   Get the status of an already submitted analysis.
      version  Display API version information.


Installation
------------

The MythX CLI runs on Python 3.6+, including 3.8-dev and pypy.

To get started, run:

.. code-block:: console

    $ pip install mythx-cli


Advanced usage
--------------

For in-depth details on how to use the MythX CLI, alternative ways to install
it, as well as helpful documentation about authentication, analyzing complex
projects and more, head over to the
`MythX CLI documentation <https://mythx-cli.readthedocs.io>`_.


The MythX CLI project is MIT-licensed and contributions are always welcome!
For more information on how to get involved, check out our
`Contribution guidelines <https://mythx-cli.readthedocs.io/en/latest/contributing.html>`_.


Useful links
------------

.. list-table::

    *   - GitHub repository
        - https://github.com/dmuhs/mythx-cli/
    *   - Documentation
        - https://mythx-cli.readthedocs.io/
    *   - Python Package Index
        - https://pypi.org/project/mythx-cli/
    *   - Current CI builds
        - https://travis-ci.org/dmuhs/mythx-cli/
    *   - Test coverage
        - https://coveralls.io/github/dmuhs/mythx-cli
