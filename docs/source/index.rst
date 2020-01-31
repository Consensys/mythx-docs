.. meta::
   :description: Learn how to integrate MythX advanced security analysis directly into development environments and build pipelines. Detect common Solidity vulnerabilities and EVM bytecode vulnerabilities automatically.

MythX User and Developer Guide
==============================

`MythX <https://mythx.io>`_ is a security analysis API for Ethereum smart contracts. It allows any developer or developer team to integrate advanced security analysis directly into development environments and build pipelines. It detects many common Solidity vulnerabilities and EVM bytecode vulnerabilities automatically.

MythX is integrated into popular developer tools you use today such as :ref:`Truffle <tools.truffle>`, :ref:`Remix <tools.remix>`, and :ref:`VS code <tools.mythxvsc>`. Plus, you can integrate MythX into your own security tools, apps, and existing blockchain services.

MythX has multiple target audiences:

* **Developers and dev teams** who wish to verify smart contract security as part of their project workflow.
* **Tool creators and integrators** who wish to build a new MythX tool or integrate the MythX API into their product or service.

.. note::

   While MythX is designed with Ethereum in mind, the service should be compatible with any chain that uses the EVM (such as VeChain and Tron). In most cases, you will just have to change a setting in your development environments to deploy to the different blockchain and then you can proceed to analyzing your contracts.

Please continue on to learn more about MythX.

Contents
--------

:ref:`getting-started`
     Test out the service, sign up for an API key, and learn about the workflow.

:ref:`tools`
     All the current and evolving tools that can be used with MythX.

:ref:`building-security-tools`
     Information about the MythX API, for developers who wish to build their own tools or integrate MythX into their product or service.

:ref:`support`
     How to get support and engage with the MythX community.


.. toctree::
   :hidden:

   getting-started/index
   tools/index
   building-security-tools/index
   getting-support/index
