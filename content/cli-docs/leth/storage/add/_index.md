+++
title = "leth storage add"
toc = true
+++
## leth storage add

Adds file to the secured IPFS storage and returns its meta file.

### Synopsis


Usage:

	leth storage add --nodeid=1 --network=rinkeby --owner=0xadC486F16F003897fb927e22438cb1b820f79879 --file=/Users/enchanterio/Documents/secret/file.txt

Possible Outputs:

	{"meta":"QmSomeIpfsHashdGXrvCgmQHo8Yqo8eLQTvC1sEJh6suBi","acl":"0x5D780255679c55846c1fE1E738e7604425171B50"}
	{"error": {"code": "SOME/INTERNAL/ERROR/CODE", "message": "explanatory error message"}}


```
leth storage add [flags]
```

### Options

```
      --file string      Absolute path to the file you want to upload to secured storage.
  -h, --help             help for add
      --network string   Possible values: 'sirius', 'mainnet', 'standalone', 'rinkeby', 'ganache'.
      --nodeid int       ID of the node in order to support multiple nodes on the same machine. 0 by default.
      --owner string     File owner address who will pay for the file ACL. The account address was generated when you signed-up.
```

### SEE ALSO

* [leth storage](/cli-docs/leth/storage/)	 - Features LethStorage's pkg capabilities over CLI such as file upload/download, access authorization...

###### Auto generated by spf13/cobra on 31-May-2019
