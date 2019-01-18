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

Here is some sample output

.. code-block:: bash

   $ truffle run analyze
  /tmp/TokenSaleChallenge.sol
    1:426  error  This binary multiply operation can result in integer overflow  SWC-101
    1:465  error  This binary add operation can result in integer overflow       SWC-101
    1:680  error  This binary multiply operation can result in integer overflow  SWC-101

  ✖ 3 problems (3 errors, 0 warnings)


.. seealso::

  * `npm package <https://www.npmjs.com/package/truffle-analyze>`_
  * `gitub project <https://github.com/consensys/truffle-analyze>`_
  * :ref:`VSCode MythX-enabled <vscode-truffle>`
