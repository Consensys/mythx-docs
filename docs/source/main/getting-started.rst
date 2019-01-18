Getting Started
===============

What is MythX?
--------------
`MythX <https://mythx.io>`_ is a security analysis API for Ethereum Smart
Contracts. It is aimed at smart contract developers to tailor security into
their Software Development Lifecycle as well as Smart Contract auditors. By
providing an easy-to-use endpoint to in-depth security analysis, MythX is
meant to turbocharge the rapid development of applications for the Ethereum
blockchain in a sustainable and secure way.

Under the hood, MythX leverages `Mythril Classic <https://github.com/ConsenSys/mythril-classic/>`_
as well as other tools we have developed in-house at `ConsenSys Diligence <https://consensys.net/diligence/>`_
to make our auditors' life easier. MythX is out way of making the combined
power of static and dynamic program analysis, as well as dynamic input
fuzzing available to the community to maintain a high security standard in
a rapidly progressing ecosystem.

For more information, announcements and support, consider joining the
`MythX Discord <https://discord.gg/kktn8Wt>`_ server.


How do I sign up?
-----------------

To use the MythX platform, a user account is required. You can register on
`our website <https://mythx.io>`_ with Metamask. Need a step-by-step guide?
Continue reading, then. Did you already register successfully? Enjoy hacking
away on our samples and tools in the developer documentation:
:ref:`DeveloperOverview`.

MythX is a SaaS product. You will need to navigate to https://mythx.io/
and create a user account.

.. image:: ../_static/mythx-main-page.png

The signup process starts by clicking the “Login with Metamask” button on the
MythX website.

.. image:: ../_static/mythx-metamask-login.jpg

Logging In
^^^^^^^^^^

On first login the user is asked to set up an API password. The user’s Ethereum
address and API password later serve as credentials for accessing the API:

- *Username:* The user’s Ethereum address
- *Password:* Chosen by the user on first signup

.. image:: ../_static/mythx-password.png

Picking a Plan
^^^^^^^^^^^^^^

New users will be directed to the license plans page. Here you can start with
a free plan. Later you can have the option to upgrade to one of several paid
plans which offer you unlimited analysis of smart contracts per day.

.. image:: ../_static/mythx-plans.jpg

Payment and Getting Started
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Payment is accepted in Ether or DAI. Note that prices are pegged to DAI, so
prices in other currencies are calculated dynamically and your payments is
converted to DAI automatically upon the selection of your payment option.

.. image:: ../_static/mythx-payment.png


*A Note on Payments:* When you purchase a plan any unused DAI will be refunded
if and when the users chooses to cancels the subscription. For example:

A user can choose 10x daily plan which fills their “fuel tank” with 10 DAI.
The MythX API tracks usage of the account and 1 DAI is burned for each 24
hours activation. Unused DAI are refunded if and when a user cancels their
subscription.

.. image:: ../_static/mythx-account.png

What's Next?
^^^^^^^^^^^^

Now that you have created your MythX account and chosen a subscription plan
you are ready to begin experiencing the power of the MythX. In the next
section, :ref:`DeveloperOverview`, you will
see three example use cases showing how you as a developer can use MythX to
thoroughly analyze your Ethereum smart contracts.


Bug Tracker
-----------

.. TODO: Write a cheeky text referring to our support endpoint

Contributing
------------

So you are an individual developer and you want to join this cool new MythX
revolution? This is the section for you.

* Gitcoin bounties.
* Discord Channels
* Links to "how to contribute" docs
