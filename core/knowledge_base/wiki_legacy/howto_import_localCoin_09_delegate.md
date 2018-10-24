## Howto import an existing delegate as witness in LocalCoin

### Preparations in LocalCoin 0.9 network

We need to Extract the signing public and private key from LocalCoin 0.9.

Let's obtain the <publickey>:

    >>> get_account <delegatename>
    [...]
    Block Signing Key: <publickey>
    [...]

Remark: Public keys in the LocalCoin network have the prefix LLC. Hence, in the case of the Graphene testnet you should replace LLC by GPH.

and the corresponding <wifkey>:

    >>> wallet_dump_account_private_key <delegatename> signing_key
    "<wifkey>"
