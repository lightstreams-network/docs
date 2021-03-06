+++
title = "leth wallet balance"
toc = true
+++
## leth wallet balance

Get account's balance in Wei.

### Synopsis


Usage:

	leth wallet balance --nodeid=1 --network=rinkeby --account=0xadc486f16f003897fb927e22438cb1b820f79879

Possible Outputs (3ETH):

	{"balance":"3000000000000000000","error":""}
	{"balance":"0","error":"some error message"}


```
leth wallet balance [flags]
```

### Options

```
      --account string   Account address to check balance for.
  -h, --help             help for balance
      --network string   Possible values: 'sirius', 'mainnet', 'standalone', 'rinkeby', 'ganache'.
      --nodeid int       ID of the node in order to support multiple nodes on the same machine. 0 by default.
```

### SEE ALSO

* [leth wallet](/cli-docs/leth/wallet/)	 - Features LethWallet's pkg capabilities over CLI such as retrieving current balance and transferring funds.

###### Auto generated by spf13/cobra on 31-May-2019
