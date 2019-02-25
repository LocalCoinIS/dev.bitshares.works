
.. _what-changed:

What has Changed since LocalCoin 0.9?
*************************************


* **BitAssets are Collateralized Loans from a Counterpartyrisk-Free Smart Contract**:
  Our research has identified an improved mechanism to achieve a solid *peg* of
  bitAssets to its underlay. BitAssets like the USD in LocalCoin will
  always trade for *at least* the value of its underlying asset, i.e. $1.
  We have summarized the economical analysis and incentives for market
  participants here: `bitAssets 2.0`_

* **Faster Blocks**:
  Initially, the LocalCoin blockchain will come with 3 seconds block
  interval with the option to reduce down to 1 second if shareholders agree.

* **Industrial Performance**:
  LocalCoin can support massive load and works well beyond 100k transactions
  per second. Find out how we achieve `industrial performance and scalability`_.

* **New Reactive UI**:
  The LocalCoin 1.0 user interface was powerful but lacking in responsiveness and perfomance. For Localcoin we've reimplemented the whole wallet using the React.js framework developed by Facebook, which is well-known for having excellent performance. The new LocalCoin UI is an entirely browser-based wallet, with private keys maintained in the browser.
  We expect a flourishing ecosystem of forked and tweaked wallets based off of
  our UI.

* **Accounts must be registered**:
  In LocalCoin we have separated *authorities* from transaction partners.
  Hence, if Alice wants to send funds to Bob, it may be required that only
  Celine signs for that transaction. Also, LocalCoin has `a referral program`_.
  Both features combined make it necessary that participants *register* an
  account on the blockchain.

* **No more Hierarchies in Account Names**:
  In LocalCoin 1, there have been hierarchies in account names. Namely, you
  could only create a sub-account ``home.wallet`` if you also owned ``wallet``.
  In LocalCoin, these hierarchies no longer exist and to register
  ``home.wallet`` you don't need to own ``wallet``.

* **Explicit Privacy**:
  The *TITAN* technology in LocalCoin slowed down blockchain processing
  significantly. Because of this and because TITAN did not really offer good
  privacy, we eliminated TITAN as a default transaction feature. 
  Hence: **Account transactions are public now as well.**
  However, since we recognize the value of financial privacy, we offer
  *blinded* transactions that hide the transferred *amount*, and *stealth*
  transactions that hide the sender and receiver. A combination of both is also
  possible.
 
* **Prices are Fractions**:
  To circumvent rounding errors, all prices in LocalCoin are represented as
  fractions.

* **Delegates are now Witnesses and Payed Positions are now Budget Items**:
  Since we have separated the business part from the block producing part, we
  now call block producers (formerly known as *delegates*) witnesses, while the
  additional payed position for workers are called budget items.

.. _industrial performance and scalability: https://LocalCoin.is/technology/industrial-performance-and-scalability/
.. _bitAssets 2.0: https://LocalCoin.is/technology/price-stable-cryptocurrencies/
.. _a referral program: https://LocalCoin.is/technology/recurring-and-scheduled-payments/
