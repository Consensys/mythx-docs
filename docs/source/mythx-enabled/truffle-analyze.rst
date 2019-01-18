.. index:: truffle-analyze
.. _truffle-analyze:

`truffle run analyze`
=====================

"Truffle" is a world-class development environment, testing framework
and asset pipeline for blockchains using the Ethereum Virtual Machine
(EVM), aiming to make life as a developer easier. Read more about it
on the `truffle suite website <https://truffleframework.com/docs/truffle/overview>`_.

We have written a `truffle "run" plugin
<https://truffleframework.com/docs/truffle/getting-started/writing-external-scripts>`_
that runs `MythX <https://mythx.io>`_ Smart Contract analyses on
truffle projects.

*Note:* This is alpha code. You will not be able to use this without a MythX
account, and will be more generally distributed in the January-February
time period.


Quickstart
----------

.. code-block:: bash

  $ truffle run analyze
  /tmp/TokenSaleChallenge.sol
    1:426  error  This binary multiply operation can result in integer overflow  SWC-101
    1:465  error  This binary add operation can result in integer overflow       SWC-101
    1:680  error  This binary multiply operation can result in integer overflow  SWC-101

  ✖ 3 problems (3 errors, 0 warnings)

Setup
-----

1. Package install
.. code-block:: bash

  $ npm install truffle-analyze

2. Enable the plugin
.. code-block:: javascript

  module.exports = {
    plugins: [ "truffle-analyze" ]
  };

3.

.. seealso::

  * `npm package <https://www.npmjs.com/package/truffle-analyze>`_
  * `github project <https://github.com/consensys/truffle-analyze>`_
  * :ref:`VSCode MythX-enabled <vscode-truffle>`
