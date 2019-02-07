+++
title = "Private file sharing"
toc = true
weight = 3
+++

## Private File Sharing for dApps, content producers

Once your Lightstreams node is fully synced and you own some ETH, you can access our most important feature!

### Private file sharing

Files are protected with ACL and access is authenticated and authorized before any content seeding starts! Not just encrypted publicly in IPFS, what majority of projects do. Privacy vs Confidentiality in action.

### Leth storage file

Each file uploaded using Leth generates 2 IPFS files.

1. A public Meta JSON file, accessible by everyone describing the protected file

```json
{
  "ext": "txt",
  "owner": "0xa92e3705e6d70cb45782bf055e41813060e4ce07",
  "hash": "QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf", // of the protected file
  "acl": "0x5D780255679c55846c1fE1E738e7604425171B50" // smart contract access rules
}
```

2. The protected file itself.

### Adding a private file

Given a file: "secret_file.txt" with content "hello secret world".

To share a private file using `leth` execute the following command:

```bash
leth storage add --nodeid=1 --network=sirius --file=$HOME/Documents/secret_file.txt --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07
```

Output:

```bash
Enter keystore's password to unlock account:

...some logs, we keep logging on DEBUG level in Alpha version for debugging early bugs

{"meta":"QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf","acl":"0xc2DBC8CdAba2df432C821639B80302f0675D6f74"}
```

Note:

- `--nodeid=1; --network=sirius` we are executing the command from Lightstreams node 1 and deploying the ACL to file on sirius network
- `--file=` flag is an absolute path to the file you want to share
- `--owner=` flag is file owner address who will pay for the file ACL. The account address was generated when you signed-up
- `"meta":"QmNkbFAo5jSKm7KLCdCr8c8ue2X53ShATD5yjyQq3ynoaf"` this is the address of a public Meta file linking to your private file in a secure IPFS storage
- `"acl"` this is the file's ACL. A smart contract addr controlling all the access rules. You can use it `leth acl grant` cmd to grant permissions to other accounts

PS: You can always run any command with `--help` flag to get explanation of all required/optional flags

```bash
leth acl grant --help
```

### Reading the private file

Now you can tell your friend who is running a different Lightstreams node to download your private file! If you would like to test it yourself, setup another Lightstreams node on the same machine in another terminal, Lightstreams node 2 and create also another account!

```bash
leth init --nodeid=2 --network=sirius
leth run --nodeid=2 --network=sirius

...wait a few hours for a full sync...
```

Once your Lightstreams node is full synced, attempt to read the private file from your new Lightstreams node 2:

```bash
leth storage fetch --nodeid=2 --network=sirius --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf --account=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

Output:

```bash
{"error": {"code": "err_cli", "message": "unable to download file to IPFS storage. Error: ipfs cat cmd timed out"}
```

This error is expected because the file owner never actually granted permission to Lightstreams node 2 account, 0xnode2ethAddr0cb45782bf055e41813060e4ce89.

Let's grant a read permission.

### Granting read access to the private file

Execute :

```bash
leth acl grant --nodeid=1 --network=sirius --permission=read --acl=0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 --account=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

Output:

```bash
{"msg":"Granting 'read' permission to account '0xnode2ethAddr0cb45782bf055e41813060e4ce89'..."}
{"msg":"Account '0xnode2ethAddr0cb45782bf055e41813060e4ce89' was granted 'read' permission."}

{"is_granted":"true"}
```

Let's try to read the `secret_file.txt` file now:

```bash
leth storage fetch --nodeid=2 --network=sirius --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf --account=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

Leth SDK will resolve the linked protected file out of the JSON Meta file and save it to a tmp directory using the hash of the protected file itself
and the extension of the uploaded file resolved from the JSON Meta file.

Output:

```bash
{"output":"/tmp/QmProtIpfsHashdGXrvCgmQHo8Yqo8eLQTvC1sEJh6suBi.txt"}
```

Congratulation, you just shared a private file over internet in a decentralised manner.

### Granting admin access to the private file

Going step further. You can also grant admin rights to other accounts, devices so they can further have the privileges of granting read/admin access to other users.

Example, let's grant an `admin` right to the Leth Node 2 account. With such a privilege, Leth Node 2 account will be able to further grant access to other devices in the network/users.

```bash
leth acl grant --nodeid=1 --network=sirius --permission=admin --acl=0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 --to=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

### Reading the public Meta file

In case you want to get information about the privately stored file, you can do so using the `leth storage meta` command.

```bash
leth storage meta --nodeid=1 --network=sirius --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf
```

Output:

```
{"filename":"secret_file.txt","ext":"txt","owner":"0xadC486F16F003897fb927e22438cb1b820f79879","hash":"QmRnXxBJg3NjXzuTi91iNYcMff4oz4NwjN7fgtBXp2UbG9","acl":"0x3cb99420c7F16f00ef41B5ace9e0C815F3736879"}
```

Note:

- `filename` is the original filename when file was uploaded
- `ext` is the original file extension
- `owner` who uploaded the file
- `hash` the hash of the protected file stored in IPFS (not the public Meta file hash)
- `acl` address of the contract handling file permissions
