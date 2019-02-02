MythX Plugin for Truffle
========================

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

.. code-block:: console

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

Add to `truffle.js`:

.. code-block:: javascript

  module.exports = {
    plugins: [ "truffle-analyze" ]
  };

For now `truffle.js` needs to be adjusted for each project. However, changes to
truffle are planned so that in the future you can specify this globally.

3. Set `MYTHX` environment variables.

Get an ETH address from `MetaMask <https://metamask.io>`_. Set the following environment variables,
adjust for your ETH address and password:

.. code-block:: bash

    export MYTHX_ETH_ADDRESS=0x1234567891235678900000000000000000000000
    export MYTHX_PASSWORD='Put your password in here!'


Using Truffle Analyze
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    $ truffle run analyze --help

    Usage: truffle run analyze [options] [*contract-name1* [*contract-name2*] ...]

    Runs MythX analyses on given Solidity contracts. If no contracts are
    given, all are analyzed.

    Options:
      --debug    Provide additional debug output
      --mode { quick | full }
                 Perform quick or in-depth (full) analysis.
      --style {stylish | unix | visualstudio | table | tap | ...},
                 Output report in the given es-lint style style.
                 See https://eslint.org/docs/user-guide/formatters/ for a full list.
      --timeout *seconds* ,
              Limit MythX analyses time to *s* seconds.
              The default is 120 seconds (two minutes).
      --version show package and MythX version information

Runs MythX analyses on given Solidity contracts. If no contracts are
given, all are analyzed.

Options are deliberately sparse since we want simple interaction. Most
of the complexity is hidden behind the MythX.

If you leave off any contract name, we'll find one inside the
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
    4:4  error  The function '_function_0xa56a3b5a' executes the SUICIDE instruction                     SWC-106
    0:0  error  Functions that do not have a function visibility type specified are 'public' by default  SWC-100

    ✖ 2 problems (2 errors, 0 warnings)

Note that in above that `analyze` may invoke `compile` when sources are not up
to date. The default report style is `stylish` however you may want to
experiment with other styles. Here is an example of using the  `table` format:

.. code-block:: console

    $ truffle+analyze analyze --style table

    /src/external-vcs/github/vulnerable-truffle-project/contracts/SimpleDAO.sol

    ║ Line     │ Column   │ Type     │ Message                                                │ Rule ID      ║
    ╟──────────┼──────────┼──────────┼────────────────────────────────────────────────────────┼──────────────╢
    ║ 12       │ 4        │ error    │ A possible integer overflow exists in the function     │ SWC-101      ║
    ║          │          │          │ '_function_0x00362a95'.                                │              ║
    ║ 17       │ 14       │ error    │ This contract executes a message call to the           │ SWC-107      ║
    ║          │          │          │ address of the transaction sender.                     │              ║
    ║ 0        │ 0        │ error    │ Contracts should be deployed with the same             │ SWC-103      ║
    ║          │          │          │ compiler version and flags that they have been         │              ║
    ║          │          │          │ tested with thoroughly.                                │              ║

    ╔════════════════════════════════════════════════════════════════════════════════════════════════════════╗
    ║ 3 Errors                                                                                               ║
    ╟────────────────────────────────────────────────────────────────────────────────────────────────────────╢
    ║ 0 Warnings                                                                                             ║
    ╚════════════════════════════════════════════════════════════════════════════════════════════════════════╝

.. seealso::

  * `npm package <https://www.npmjs.com/package/truffle-analyze>`_
  * `github project <https://github.com/consensys/truffle-analyze>`_