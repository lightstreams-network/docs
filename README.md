# docs.lightstreams.network

## Prerequisite

### Install Hugo

1. Go to the [Hugo releases](https://github.com/gohugoio/hugo/releases) and grab the
correct version

2. Follow [installation instructions](https://gohugo.io/getting-started/installing)

3. Check hugo is installed correctly

```
hugo version
```

## Getting started

### Clone this repository
```
git clone git@github.com:lightstreams-network/docs.git
```

### Edit files in `content`
Once you have Hugo installed, you can start editing the files in the `content`
folder.

### Run local server to check changes
```
hugo server
```

### Publish changes
```
hugo
```

### Deploy changes

```
./deploy-gh-pages
```

### Commit

```
git add .
git commit -m "Updated xyz"
```

## Update CLI docs

Run the create-cli-docs command (for lightstreams developers only:
```
./bin/create-cli-docs
```
Once this is done, follow the instructions above to publish the changes.

