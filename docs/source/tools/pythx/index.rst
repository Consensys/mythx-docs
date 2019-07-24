PythX - A Python MythX CLI
==========================

The `PythX package <https://pypi.org/project/pythx/>`_ does not only provide
a kickass Python library, but also ships with a command line interface by
default. While it initially was meant as an example to show developers how easy
it is to implement complex behaviour with the PythX library, it has since taken
on a life on its own. While the focus clearly is on the library side of PythX,
we have decided to also maintain the CLI part of it as a low-level entrypoint
to new users who just want to play around with the API.


Installation
------------
PythX runs on Python 3.5+.

To get started, simply run

.. code-block:: console

    $ pip3 install pythx

The PythX CLI
-------------
The PythX CLI aims to be a simple example implementation to show developers by
practical example how PythX can be used in action. It provides a simple (and
pretty!) interface to list analyses, submit new ones, check the status of a
job, and get report data on the found issues.

.. code-block:: console

    $ pythx
    Usage: pythx [OPTIONS] COMMAND [ARGS]...

      PythX is a CLI/library for the MythX smart contract security analysis API.

    Options:
      --help  Show this message and exit.

    Commands:
      check    Submit a new analysis job based on source code, byte code, or...
      login    Login to your MythX account
      logout   Log out of your MythX account
      openapi  Get the OpenAPI spec in HTML or YAML format
      ps       Get a greppable overview of submitted analyses
      refresh  Refresh your MythX API token
      report   Check the detected issues of a finished analysis job
      status   Get the status of an analysis by its UUID
      top      Display the most recent analysis jobs and their status
      truffle  Submit a Truffle project to MythX
      version  Print version information of PythX and the API


By default, PythX comes with a pre-enabled trial user. To get started right
away, simply login with the default values:

.. code-block:: console

    $ pythx login
    Please enter your Ethereum address [0x0000000000000000000000000000000000000000]:
    Please enter your MythX password [trial]:
    Successfully logged in as 0x0000000000000000000000000000000000000000

If you already have an account on `MythX <https://mythx.io>`_, simply login with your Ethereum
address and the API password you have set on the website.

Submit an Solidity source file for analysis:

.. code-block:: console

    $ pythx check -sf /mythx-test/contracts/etherstore.sol
    Analysis submitted as job df137587-7fc1-466a-a4b2-d63392099682


Check the status of your analysis job:

.. code-block:: console

    $ pythx status df137587-7fc1-466a-a4b2-d63392099682
    ╒════════════════╤══════════════════════════════════════╕
    │ uuid           │ df137587-7fc1-466a-a4b2-d63392099682 │
    ├────────────────┼──────────────────────────────────────┤
    │ apiVersion     │ v1.4.3                               │
    ├────────────────┼──────────────────────────────────────┤
    │ mythrilVersion │ 0.20.0                               │
    ├────────────────┼──────────────────────────────────────┤
    │ maestroVersion │ 1.2.3                                │
    ├────────────────┼──────────────────────────────────────┤
    │ harveyVersion  │ 0.0.13                               │
    ├────────────────┼──────────────────────────────────────┤
    │ maruVersion    │ 0.3.4                                │
    ├────────────────┼──────────────────────────────────────┤
    │ queueTime      │ 0                                    │
    ├────────────────┼──────────────────────────────────────┤
    │ runTime        │ 0                                    │
    ├────────────────┼──────────────────────────────────────┤
    │ status         │ Finished                             │
    ├────────────────┼──────────────────────────────────────┤
    │ submittedAt    │ 2019-03-05T10:24:05.071Z             │
    ├────────────────┼──────────────────────────────────────┤
    │ submittedBy    │ 123456789012345678901234             │
    ╘════════════════╧══════════════════════════════════════╛


Get the analysis report:

.. code-block:: console

    $ pythx report df137587-7fc1-466a-a4b2-d63392099682
    Report for /mythx-test/contracts/etherstore.sol
    ╒════════╤══════════════════════╤════════════╤═════════════════════════════════════════════════════╕
    │   Line │ SWC Title            │ Severity   │ Short Description                                   │
    ╞════════╪══════════════════════╪════════════╪═════════════════════════════════════════════════════╡
    │     21 │ Reentrancy           │ High       │ persistent state read after call                    │
    ├────────┼──────────────────────┼────────────┼─────────────────────────────────────────────────────┤
    │     21 │ Reentrancy           │ High       │ persistent state write after call                   │
    ├────────┼──────────────────────┼────────────┼─────────────────────────────────────────────────────┤
    │     22 │ Reentrancy           │ High       │ persistent state write after call                   │
    ├────────┼──────────────────────┼────────────┼─────────────────────────────────────────────────────┤
    │     19 │ Reentrancy           │ Medium     │ A call to a user-supplied address is executed.      │
    ├────────┼──────────────────────┼────────────┼─────────────────────────────────────────────────────┤
    │     19 │ Timestamp Dependence │ Low        │ Sending of Ether depends on a predictable variable. │
    ╘════════╧══════════════════════╧════════════╧═════════════════════════════════════════════════════╛

