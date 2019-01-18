.. _DeveloperOverview:

MythX for Developers
====================

Welcome, fellow hackers! Here you will find an overview of how we make the
MythX platform available in (hopefully) your programming language and IDE
of choice. Did not find what you were looking for? Check out how you can add
your solution to this documentation in the contribution guidelines:
:ref:`Submit Your Own Tool!`.

Note that whatever you might find here, the `MythX OpenAPI Spec <https://staging.api.mythx.io/v1/openapi>`_
is the specification and ultimate authority. Beyond that be dragons.

.. contents:: :local:


Using the API from the Shell
----------------------------

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


Installation
^^^^^^^^^^^^

To run the shell scirpt here, you need a couple of command-line utility
programs:

* `bash <https://www.gnu.org/software/bash/>`_,
* `curl <https://curl.haxx.se/download.html>`_ to make the HTTPS requests, and
* `jq <https://stedolan.github.io/jq/download/>`_ to make the JSON output prettier

Most OS's have these available. Run `./prerequisites.sh` to double check
though.

After ensuring you have the prerequistes programs, set
`MYTHRIL_PASSWORD` to and one of `EMAIL` or `MYTHRIL_ETH_ADDRESS` to
values that have been registered. For example:

.. code-block:: console

  $ export MYTHRIL_PASSWORD=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

  $ # Only one of two below is needed:
  $ export EMAIL=me@example.com
  $ export MYTHRIL_ETH_ADDRESS=0x.............

Above `MYTHRIL_API_URL` is optional and the default value is given above.
We have however a number of API servers. If you are using one or using
your own private version, set the URL host accordiatingly.


Examples
^^^^^^^^

Once you are set up, you can:

* Submit a contract for analysis, creating a job run with a UUID
* See the status of job using the UUID of a previously submitted analysis
* Get the results of a previously finished analysis using the UUID
* See a list of previously submitted analyses
* Get the current versions of Mythril API and its core sub-modules
* Get the OpenAPI specification


To submit a job for use `analyses.sh` for analysis:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./analyses.sh sample-json/PublicArray.js
  Issuing HTTP POST http://api.mythril.ai/v1/analyses
    (with MYTHRIL_API_KEY and EVM bytecode)
  curl completed sucessfully. Output follows...
  HTTP/1.1 200 OK
  {
    "result": "Queued",
    "uuid": "bf9fe267-d322-4641-aae2-a89e62f40770"
  }


To job status of a job run (UUID)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./analyses-status.sh "bf9fe267-d322-4641-aae2-a89e62f40770"
  Issuing HTTP GET http://api.mythril.ai/v1/analyses/bf9fe267-d322-4641-aae2-a89e62f40770
    (with MYTHRIL_API_KEY)
  curl completed sucessfully. Output follows...
  HTTP/1.1 200 OK
  {
    "result": "Finished",
    "uuid": "bf9fe267-d322-4641-aae2-a89e62f40770"
  }


To see the results of status:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./analyses-results.sh "bf9fe267-d322-4641-aae2-a89e62f40770"
  Issuing HTTP GET http://api.mythril.ai/v1/analyses/bf9fe267-d322-4641-aae2-a89e62f40770/issues
  curl completed sucessfully. Output follows...
  HTTP/1.1 200 OK
  [
    {
      "address": 499,
      "contract": "MAIN",
      "debug": "callvalue: 0xd7ee0142c5f24581862400cc4785a2910417ad282802609755ac30ac4c9e435d\nstorage_keccac_1461501637330902918203684832716283019655932542975_&\n1461501637330902918203684832716283019655932542975_&\n1461501637330902918203684832716283019655932542975_&\ncalldata_MAIN[4]: 0x744240060f11ee8302555055dccca6b72611ae29090e239231b0a7b8f29ae057\ncalldata_MAIN[0]: 0x362a9500000000000000000000000000000000000000000000000000000000\ncalldatasize_MAIN: 0x4\n",
      "description": "A possible integer overflow exists in the function `fallback`.\nThe addition or multiplication may result in a value higher than the maximum representable integer.",
      "function": "fallback",
      "title": "Integer Overflow",
      "type": "Warning"
    },
    {
      "address": 648,
      "contract": "MAIN",
      "debug": "",
      "description": "This contract executes a message call to the address of the transaction sender. Generally, it is not recommended to call user-supplied addresses using Solidity's call() construct. Note that attackers might leverage reentrancy attacks to exploit race conditions or manipulate this contract's state.",
      "function": "_function_0x2e1a7d4d",
      "title": "Message call to external contract",
      "type": "Warning"
    },
    ...
  ]


Get the API version number
^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: console

  $ ./api-version.sh
  Issuing HTTP GET https://api.mythril.ai/v1/version
  curl completed sucessfully. Output follows...
  HTTP/1.1 200 OK
  v1.0.20


Get the OpenAPI specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

  $ ./get-openapi-spec.sh
  Issuing HTTP GET https://api.mythril.ai/v1/openapi.yaml
  curl completed sucessfully. Output follows...
  HTTP/1.1 200 OK
  -----------------------------------
  openapi: 3.0.1
  servers:
    - url: 'https://api.mythril.ai/v1'
  ...

.. seealso::

  * `The github project <https://github.com/rocky/mythx-api-curl>`_
  * `MythX API spec <https://staging.api.mythx.io/v1/openapi/>`_


JavaScript SDK
--------------

If you want to add MythX analysis into a JavaScript-based program as
we have done to truffle in :ref:`Truffle Analyze Plugin`, or
:ref:`VSCode Solidity Extension`, you can use the same libraries that we use.

A thin wrapper around the MythX API is called `armlet`. We are also working on
a more beefy software development kit for Javascript called `mythx-js-sdk`.

.. toctree::
    :maxdepth: 1

    ../tooling/armlet
    ../tooling/mythx-js-sdk
    ../tooling/ramuh
    ../tooling/sabre


Golang SDK
----------

Shard is a lightweight Golang CLI for MythX. It serves as a reference
implementation.

Installation (unstable)
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    snap install --devmode --edge shard

Configuration
^^^^^^^^^^^^^

You can put a config file in `$HOME/.config/.shard.yaml` containing your api
key. `shard.yaml` contains:

.. code-block:: yaml

    api-key: <put your api key here>

This way you don't have to put it in the cli every time. Alternatively shard
also looks in the current directory for a configuration file if it can't find
one in the aforementioned directory.

Using Shard
^^^^^^^^^^^

As any with any tool, the help command can be very useful

.. code-block:: console

    $ shard
    Shard is a mythril light client

    Usage:
    shard [command]

    Available Commands:
    analyze     Analyzes the contract
    help        Help about any command
    version     Print the version number of Shard

    Flags:
    -k, --api-key string   The api key to authenticate with. Overrides config value.
        --config string    config file (default is $HOME/.config/.shard.yaml)
    -h, --help             help for shard
    -v, --verbose          Enable verbose logging.

    Use "shard [command] --help" for more information about a command.

To analyze a contract execute:
.. code-block:: console

    $ shard analyze 0x606b...


Python SDK
----------


Truffle Analyze Plugin
----------------------

Truffle is a world-class development environment, testing framework
and asset pipeline for blockchains using the Ethereum Virtual Machine
(EVM), aiming to make life as a developer easier. Read more about it
on the `Truffle Suite website <https://truffleframework.com/docs/truffle/overview>`_.

We have written a `truffle "run" plugin
<https://truffleframework.com/docs/truffle/getting-started/writing-external-scripts>`_
that runs `MythX <https://mythx.io>`_ Smart Contract analyses on
truffle projects.

*Note:* This is alpha code. You will not be able to use this without a MythX
account, and will be more generally distributed in the January-February
time period.

Quickstart
^^^^^^^^^^

.. code-block:: bash

  $ truffle run analyze
  /tmp/TokenSaleChallenge.sol
    1:426  error  This binary multiply operation can result in integer overflow  SWC-101
    1:465  error  This binary add operation can result in integer overflow       SWC-101
    1:680  error  This binary multiply operation can result in integer overflow  SWC-101

  ✖ 3 problems (3 errors, 0 warnings)

Setup
^^^^^

1. Package install

.. code-block:: bash

  $ npm install truffle-analyze

2. Enable the plugin

.. code-block:: javascript

  module.exports = {
    plugins: [ "truffle-analyze" ]
  };

For now `truffle.js` needs to be adjusted for each project. However, changes to
truffle are planned so that in the future you can specifiy this globally.

3. Set `MYTHX` environment variables.

Get an ETH address from `MetaMask <https://metamask.io>`_. Set the following enviromment variables,
adjust for your ETH address and password:

.. code-block:: console

    export MYTHRIL_ETH_ADDRESS=0x1234567891235678900000000000000000000000
    export MYTHRIL_PASSWORD='Put your password in here!'

Using Truffle Analyze
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    $ truffle run analyze help

    Usage:        truffle run analyze [options] [*contract-name1* [contract-name2*] ...]
    Description:  Run MythX analyses on a contract
    Options:
        --debug     Provide additional debug output
        --mode { quick | full }
                    Perform quick or or in-depth (full) analysis
        --style {stylish | unix | visualstudio | table | tap | ...}
                    Output reort in the given es-lint style.
                    See https://eslint.org/docs/user-guide/formatters/ for a full list.
        --timeout *seconds* ,
                    Limit MythX analysis time to *s* seconds.
                    The default is 120 seconds (two minutes).
        --version  Show package and MythX version information.

Runs MythX analyses on given Solidity contracts. If no contracts are
given, all are analyzed.

Options are deliberately sparse since we want simple interaction. Most
of the complexity is hidden behind the MythX.

If you leave off a *contract-name*, we'll find one inside the
project. If you have more than one contract in the project you should
specify which one you want to use. Instead of a contract name inside a
solidity file, you can also give either a relative or absolute path
the a JSON file the `build/contracts` directory. This is useful if
you are running inside a shell that contains command completion.

Here is an example:

.. code-block:: console

    $ truffle run analyze SimpleSuicide
    Compiling ./contracts/Migrations.sol...
    Compiling ./contracts/SimpleDAO.sol...
    Compiling ./contracts/simple_suicide.sol...
    Compiling ./contracts/suicide.sol...

    /tmp/github/vulnerable-truffle-project/contracts/SimpleSuicide.sol
    4:4  error  The function '_function_0xa56a3b5a' executes the SUICIDE instruction                     mythril/SWC-106
    0:0  error  Functions that do not have a function visibility type specified are 'public' by default  maru/SWC-100

    ✖ 2 problems (2 errors, 0 warnings)

Note that in above that `analyze` may invoke `compile` when sources are not up
to date. The default report style is `stylish` however you may want to
experiment with other styles. Here is an example of using the  `table` format:

.. code-block:: console

    $ truffle+analyze analyze --style table

    /src/external-vcs/github/vulnerable-truffle-project/contracts/SimpleDAO.sol

    ║ Line     │ Column   │ Type     │ Message                                                │ Rule ID              ║
    ╟──────────┼──────────┼──────────┼────────────────────────────────────────────────────────┼──────────────────────╢
    ║ 12       │ 4        │ error    │ A possible integer overflow exists in the function     │ mythril/SWC-101      ║
    ║          │          │          │ '_function_0x00362a95'.                                │                      ║
    ║ 17       │ 14       │ error    │ This contract executes a message call to the           │ mythril/SWC-107      ║
    ║          │          │          │ address of the transaction sender.                     │                      ║
    ║ 0        │ 0        │ error    │ Contracts should be deployed with the same             │ maru/SWC-103         ║
    ║          │          │          │ compiler version and flags that they have been         │                      ║
    ║          │          │          │ tested with thoroughly.                                │                      ║

    ╔════════════════════════════════════════════════════════════════════════════════════════════════════════════════╗
    ║ 3 Errors                                                                                                       ║
    ╟────────────────────────────────────────────────────────────────────────────────────────────────────────────────╢
    ║ 0 Warnings                                                                                                     ║
    ╚════════════════════════════════════════════════════════════════════════════════════════════════════════════════╝

.. seealso::

  * `npm package <https://www.npmjs.com/package/truffle-analyze>`_
  * `github project <https://github.com/consensys/truffle-analyze>`_
  * :ref:`VSCode Truffle Extension`


.. _VSCodeSolidity:

VSCode Solidity Extension
-------------------------

We are currently working with Juan Blanco to get this into his `VScode Solidity Extension <https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity>`_.
The `current working code can be found on github <https://github.com/rocky/vscode-solidity>`_.


.. _VSCodeTruffle:

VSCode Truffle Extension
------------------------

We are currently working with Microsoft to get this into the planned Microsoft VSCode extension for Truffle.
Note: in contrast to `truffle-analyze <https://github.com/ConsenSys/truffle-analyze>`_, this integrates MythX's reports into the VSCode's IDE.


Remix IDE Plugin
----------------

Remix is a powerful, open source tool that helps you write Solidity contracts straight from the browser. Written in JavaScript, Remix supports both usage in the browser and locally.
Read more about it `here <https://remix.readthedocs.io/en/latest/>`_.

MythX integration into Remix should be done sometime this year.


Submit Your Own Tool!
---------------------

Oh no! You *love* developing in `Piet <https://esolangs.org/wiki/Piet>`_ but
there is no MythX library available? If you come up with your own cool
solution, we would like to know about it. You can head on over to our developer
guide `Github repository <https://github.com/ConsenSys/mythx-developer-guide>`_
and make a Pull Request. Make sure to check out the contribution guidelines to
get it merged even more quickly.
