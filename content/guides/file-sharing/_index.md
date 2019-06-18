+++
title = "Private file sharing"
toc = true
weight = 1
+++

Once your Lightstreams node is fully synced and you own some PHT(or ETH),
you can start distributing files! If you still don't have a Lightstreams node
running locally and fully synchronize, follow [the instructions here](/getting-started/quick-start/)

## Private File Sharing for dApps, content producers

Files are protected using Access Control List(ACL) and every access is authenticated and authorized
before any content seeding starts! Not just encrypted publicly in IPFS,
what majority of projects do. Privacy vs Confidentiality in action.

### Storage files

Each file uploaded using Leth generates 2 IPFS files:

1. The uploaded file itself. (`/tmp/secret_file.txt)
1. A public metadata document(`meta`, in json format, describing the protected file

### # Adding a private file

Given a file such as "/tmp/secret_file.txt", with content `Hello secret world`.

To share a private file using `leth` execute the following command:

```bash
leth storage add --nodeid=1 --network=sirius --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 \
 --file=/tmp/secret_file.txt
```

Where:

- `--nodeid=1; --network=sirius` identifies the lightstreams node running at this time locally
- `--file=` flag is an absolute path to the file you want to share
- `--owner=` flag is file owner address who will pay for the file ACL. The account address was generated when you signed-up


We insert the passphrase for the account `0xa92e3705e6d70cb45782bf055e41813060e4ce07`
```bash
Enter keystore password to unlock account:
```

We will obtain a similar output as following:
```bash
...some logs, we keep logging on DEBUG level in Alpha version for debugging early bugs
File successfully uploaded to IPFS storage.	{"meta": "QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf"}
{"meta":"QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf","acl":"0xc2DBC8CdAba2df432C821639B80302f0675D6f74"}
```

  Note:

- `"meta"` this is the address of a public Meta file linking to your private file in a secure IPFS storage
- `"acl"` this is the file's ACL. A smart contract addr controlling all the access rules. You can use it [`leth acl grant`](#granting-read-access-to-the-private-file) cmd to grant permissions to other accounts

#### Using Curl

Alternative you could also do a HTTP API call:
```bash
$>  curl -X POST \
  http://localhost:9091/storage/add \
  -H 'Content-Type: multipart/form-data' \
  -F owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 \
  -F password=password \
  -F file="@/tmp/secret_file.txt"

{"meta":"QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf","acl":"0xc2DBC8CdAba2df432C821639B80302f0675D6f74"}
```

To do that you should have run your local Lightstreams node using `--https`
to enable the HTTP API.

### # Reading the private file

Now you can tell your friend who is running another Lightstreams node on his computer to download your private file!

For testing proposed you may setup another Lightstreams node locally, using a different `nodeid` and on the same network, as follow:

```bash
leth init --nodeid=2 --network=sirius
leth run --nodeid=2 --network=sirius [--https]

...wait a few minutes for a full sync...
```

Once your Lightstreams node is full synced, attempt to read the private file from your new Lightstreams node 2:

```bash
leth storage fetch --nodeid=2 --network=sirius --account=0xnode2ethAddr0cb45782bf055e41813060e4ce89 \
  --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf
```

Output:

```bash
{"error": {"code": "err_cli", "message": "unable to download file to IPFS storage. Error: ipfs cat cmd timed out"}
```

This error is expected because the file owner never actually granted permission to Lightstreams node 2 account, `0xnode2ethAddr0cb45782bf055e41813060e4ce89`.

Let's grant a read permission.

#### Using Curl

In order to read documents using the HTTP API you first need to request a token as follow:
```bash
$> curl -X POST \
  http://localhost:9092/user/signin \
  -H 'Content-Type: application/json' \
  -d '{"account":"0xnode2ethAddr0cb45782bf055e41813060e4ce89","password":"password"}'

{ token: "eyJibG9ja2NoYWluIjoiRVRIIiwiZX..." }
```

Then we use the token to request the file access
```bash
$> curl -X GET \
  'http://localhost:9092/storage/fetch?meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf&token=eyJibG9ja2NoYWluIjoiRVRIIiwiZX...' \
  --output /tmp/secret_file_copy.txt
  
{"error": {"code": "err_cli", "message": "unable to download file to IPFS storage. Error: ipfs cat cmd timed out"}
```

### # Granting read access to the private file

Only the owner of the file can grant access to its files. In this case we go back to the original terminal
where owner account was set and execute the following command:

```bash
leth acl grant --nodeid=1 --network=sirius --permission=read --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 \
--acl=0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E --to=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```
Where:

- `acl` corresponds to the smart contract address provided after we published the file
- `to` is the account we are granting access to
- `permission` is the permission to grant, it may be: ['read', 'write', 'admin']

Output:

```bash
{"msg":"Granting 'read' permission to account '0xnode2ethAddr0cb45782bf055e41813060e4ce89'..."}
{"msg":"Account '0xnode2ethAddr0cb45782bf055e41813060e4ce89' was granted 'read' permission."}

{"is_granted":"true"}
```

Let's go back to the second account terminal, and try to read the `secret_file.txt` file now:

```bash
leth storage fetch --nodeid=2 --network=sirius --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf --account=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

Leth SDK will resolve the linked protected file out of the JSON Meta file and save it to a tmp directory using the hash of the protected file itself
and the extension of the uploaded file resolved from the JSON Meta file.

Output:

```bash
{"output":"/tmp/secret_file.txt"}
```

Congratulation, you just shared a private file over Internet in a decentralised manner.

PS: You can always run any command with `--help` flag to get explanation of all required/optional flags

```bash
leth acl grant --help
```

#### Using Curl

As it is explained above using the CLI, we could do the same using curl to grant
read access to the user _0xnode2ethAddr0cb45782bf055e41813060e4ce89_: 
```bash
$> curl -X POST \
  http://localhost:9091/acl/grant \
  -H 'Content-Type: application/json' \
  -d '{"acl":"0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E", "owner":"0xa92e3705e6d70cb45782bf055e41813060e4ce07", "password":"password", "to":"0xnode2ethAddr0cb45782bf055e41813060e4ce89", "permission": "read"}'

{"is_granted":"true"}
```

Then we try again to fetch the file using same token obtained above:
```bash
$>  curl -X GET \
  'http://localhost:9092/storage/fetch?meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf&token=eyJibG9ja2NoYWluIjoiRVRIIiwiZX...' \
  --output /tmp/secret_file_copy.txt
```
this time no error output is returned and file content is stored at `/tmp/secret_file_copy.txt`.

### # Granting admin access to the private file

Going step further. You can also grant ``admin` rights to other accounts, devices so they can further have the privileges of granting read/admin access to other users.

Example, let's grant an `admin` right to the Leth Node 2 account. With such a privilege, Leth Node 2 account will be able to further grant access to other devices in the network/users.

```bash
leth acl grant --nodeid=1 --network=sirius --permission=admin --acl=0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E --owner=0xa92e3705e6d70cb45782bf055e41813060e4ce07 --to=0xnode2ethAddr0cb45782bf055e41813060e4ce89
```

#### Using Curl
```bash
$> curl -X POST \
  http://localhost:9091/acl/grant \
  -H 'Content-Type: application/json' \
  -d '{"acl":"0x2F15B633b4bC41BdFBBD8AAf2Be7Dae958D27C7E", "owner":"0xa92e3705e6d70cb45782bf055e41813060e4ce07", "password":"password", "to":"0xnode2ethAddr0cb45782bf055e41813060e4ce89", "permission": "admin"}'

{"is_granted":"true"}
```

### # Reading the public Meta file

In case you want to get information about the privately stored file, you can do so using the `leth storage meta` command.

```bash
leth storage meta --nodeid=1 --network=sirius --meta=QmZYSewpHNvdW1TTgska792QAT7Yd6yxZAoybpYFskTZSf
```

Output:

```json
{
 "filename":"secret_file.txt",
 "ext":"txt",
 "owner":"0xadC486F16F003897fb927e22438cb1b820f79879",
 "hash":"QmRnXxBJg3NjXzuTi91iNYcMff4oz4NwjN7fgtBXp2UbG9",
 "acl":"0x3cb99420c7F16f00ef41B5ace9e0C815F3736879"
}
```

Note:

- `filename` is the original filename when file was uploaded
- `ext` is the original file extension
- `owner` who uploaded the file
- `hash` the hash of the protected file stored in IPFS (not the public Meta file hash)
- `acl` address of the contract handling file permissions

