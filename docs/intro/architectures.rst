
******************************
Introduction & Architectures
******************************


Welcome to LocalCoin! In this section, we are looking into the LocalCoin Architecture overview (entities and structures), and how the Core team processes the development work.

If developers who are interested in contributing to the Core team, they might want to check the Contribution Guide and the GitFlow to understand how LocalCoin-Core team handles the repository files and branches.  The Core team current project, issues, and releases plans are located in the LocalCoin Core repository under the Issues and the Projects tabs.m.

.. contents:: Table of Contents
   :local:

-------



LocalCoin Members
===================

If you have a LocalCoin account, you are a LLC Holder, and you have a voting power to make decisions in the LocalCoin Community. (Read more: :ref:`LocalCoin Accounts <llc-accounts>` )



.. image:: ../../_static/structures/llcholders-v1.png
        :alt: LocalCoin Architecture
        :width: 700px
        :align: center

----------------

LocalCoin Architecture
==========================

GitHub Repositories and Entities
------------------------------------

This is an overview of LocalCoin Architecture image. The purpose of this image is to bring the main elements together and share what types of resources you might find in the LocalCoin Github repositories.

.. image:: ../../_static/structures/localcoin-architecture-v3notop.png
        :alt: LocalCoin Architecture
        :width: 650px
        :align: center

----------------

Key Design Concepts and the Features
=========================================

The below image is an overview of LocalCoin Architecture. The purpose of this image is to bring the main elements together and share what types of resources you might find in the LocalCoin Github repositories.

Key points and fundamentals for the design:
---------------------------------------------

- Keep everything in memory.
- Keep the core business logic in a single thread.
- Keep cryptographic operations (hashes and signatures) out of the core business logic.
- Divide validation into state-dependent and state-independent checks.
- Use an object-oriented data model.
- Avoid synchronization primitives (locks, atomic operations)
- Minimize unnecessary computation in the business logic processor.

LocalCoin is built to aim high-performance blockchain and has been done to remove all calculations that are not part of the critical, order-dependent, evaluation from the core business logic, and to design a protocol the facilitates these kinds of optimizations.


LocalCoin Available Features
--------------------------------

LocalCoin can be made to function as a software, a network, a ledger, a bank, an exchange, and a currency all at once. (e.g., It can fulfill the role of a bank by maintaining a distributed ledger that tracks debt collateralized by other assets. You can find out that LocalCoin offers numerous features that are not available on other popular blockchain platforms.

* **SmartCoins** are fungible, divisible and free from any restrictions. A SmartCoin is a cryptocurrency whose value is pegged to that of another asset, such as the US Dollar or gold. SmartCoins implement the concept of a collateralized loan and offer it on the blockchain.
* **Decentralized Exchange** - LocalCoin provides a high-performance decentralized exchange, with all the features you would expect in a trading platform.

  - Secure: All of the reserves are kept as LLC held on the blockchain, and they cannot be stolen, because there are no private keys that can be compromised to steal the reserves.

* Trading / Financial Services
* Transferable Named Account (human-friendly account name)
* Globally unique account name and ID.
* Dynamic Account Permissions
* Multi-user control for account
* Two authorities: owner and active keys
* Transaction + multi-signature authority
* **Proposed transaction infrastructure**

  - witch tracks partially approved transactions.
  - It can be used for a scheduled payment

* Fees calculation

  - Transaction fee
  - Fee Schedules

* Assets - **User Issues Asset (UIA)**

  - to help facilitate profitable business models for certain types of services.
  - *Use Cases* (Event tickets, Reward points, privatized SmartCoins, Predictions Market, more).
  - How to profit (i.e.,Fee pools)

* BitAsset - USD, EUR, CNY, and others.
* **Delegated Proof of State Consensus (DPOS)**

  - Under DPOS, LLC Holder has influence.
  - A robust and flexible consensus protocol.

* Block Production by Elected witnesses
* **Referral Program** - to incentivize people to bring in more people.
* Vesting valance

----------------

Transactions and Performance
===============================

Localcoin Block Explorer
-------------------------------

LocalCoin Explorer shows LocalCoin Blockchain information. You can observe LocalCoin Blockchain *Health* Status (head_block_num, head_block_age, chain_id, etc.), how transactions processing, assets volume, and members.

If you would like to see more detailed information, the LLC.is offers other information tabs (i.e., Operations, Proxies, Markets, SmartCoins, UIAs, and Holders) to view.

- `LLC.is  <https://www.LLC.is/>`_


Blockchain Activity
---------------------

Blockchain Activity Matrix shows different tokens (assets) *Activity*, *Value*, and *Index*. It's interesting to check the CUI index is Capacity Utilization Index (a rate of blockchain daily activity to total blockchain capacity) to see how much numbers LocalCoin has.

- `Block'tivity <http://blocktivity.info/>`_


|

|
