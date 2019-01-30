+++
title = "leth storage fetch"
toc = true
+++
## leth storage fetch

Downloads file content from secured IPFS storage based on the meta file.

### Synopsis


Usage:

	leth storage fetch --nodeid=1 --network=rinkeby --account=0xadC486F16F003897fb927e22438cb1b820f79879 --meta=QmZnx4FPooZoy2kTFzAKhZAzhuQ3EHG8yx2E57GvN2t1vb

Possible Outputs:

	{"output":"/tmp/secret/file.txt"}
	{"error": {"code": "internal error code", "message": "explanatory error message"}}


```
leth storage fetch [flags]
```

### Options

```
      --account string             The account address who should be authorized against the content's ACL. The account address was generated when you signed-up.
  -h, --help                       help for fetch
      --meta leth storage upload   IPFS file hash of content you want to read from secured storage returned by leth storage upload command.
      --network string             Possible values: 'rinkeby, ganache, sirius'.
      --nodeid int                 ID of the node in order to support multiple nodes on the same machine. 0 by default.
```

### SEE ALSO

* [leth storage](/04.cli-docs/leth/storage/)	 - Features LethStorage's pkg capabilities over CLI such as file upload/download, access authorization...

###### Auto generated by spf13/cobra on 17-Dec-2018