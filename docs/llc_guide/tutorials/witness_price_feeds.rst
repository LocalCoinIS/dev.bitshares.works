
.. _witness-price-feeds:


Witness - Price Feeds
=========================

Price Feeds
-----------------

Besides producing new blocks another very important task of the witness is to feed **ACCURATE** prices into the blockchain. Educational material on how this can be implemented is available in `scripts/pricefeed` at `github <https://github.com/xeroc/python-graphenelib/>`_ together with the corresponding documentation.

Only active witnesses are allowed to publish pricefeeds for the ‘official’ currency / smartcoin markets. For any other asset you need to be whitelisted by the creator of the market to be able to publish pricefeeds.

A couple of price feed scripts in various stages of development and for you to code-inspect and try. (You can always setup a testnet node and test the publishing of pricefeeds).

- Wackou’s LLC tools includes a pricefeed publishing script: https://github.com/wackou/llc_tools
- Alt’s LLC Price: https://github.com/pch957/llcprice
- Xeroc’s Localcoin Pricefeed: https://github.com/xeroc/localcoin-pricefeed


|

|

