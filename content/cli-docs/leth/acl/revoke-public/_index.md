+++
title = "leth acl revoke-public"
toc = true
+++
## leth acl revoke-public

Revoke a public read access from everybody.

### Synopsis


Usage:

	leth acl revoke-public --nodeid=1 --network=rinkeby --acl=0xd966aa573f8AcBfEb3724B661B420c258ceA5D38 --owner=0xadC486F16F003897fb927e22438cb1b820f79879

Possible Outputs:

	{"is/revoked":"true"}
	{"error": {"code": "SOME/INTERNAL/ERROR/CODE", "message": "explanatory error message"}}


```
leth acl revoke-public [flags]
```

### Options

```
      --acl string       ACL ID (Deployed Smart Contract Hex Addr) associated with the stored file.
  -h, --help             help for revoke-public
      --network string   Possible values: 'sirius', 'mainnet', 'standalone', 'rinkeby', 'ganache'.
      --nodeid int       ID of the node in order to support multiple nodes on the same machine. 0 by default.
      --owner string     The account with rights to grant the ACL permission.
```

### SEE ALSO

* [leth acl](/cli-docs/leth/acl/)	 - Features LethACL's pkg capabilities over CLI such as granting ACL permissions.

###### Auto generated by spf13/cobra on 31-May-2019