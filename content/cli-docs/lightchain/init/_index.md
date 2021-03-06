+++
title = "lightchain init"
toc = true
+++
## lightchain init

Initializes new lightchain node according to the configured flags.

### Synopsis

Initializes new lightchain node according to the configured flags.

```
lightchain init [flags]
```

### Options

```
      --datadir string   Data directory for the databases and keystore (default "/home/ggarrido/.lightchain")
      --force            Forces the init by removing the data dir if already exists
  -h, --help             help for init
      --lvl string       Level of logging (default "info")
      --mainnet          Initialize a node connected to production, MainNet
      --sirius           Initialize a node connected to Sirius network
      --standalone       Data directory for the databases and keystore
      --trace            Whenever to be asserting and reporting blockchain state in real-time (testing, debugging purposes)

```

### SEE ALSO

* [lightchain](/cli-docs/lightchain/)	 - Lightstreams PoA blockchain node.

###### Auto generated by spf13/cobra on 27-Feb-2019
