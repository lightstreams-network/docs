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
git clone --recurse-submodules git@github.com:lightstreams-network/docs.git
cd docs/public
git checkout master
cd ..
```

## Update docs

### Edit files in `content`
Once you have Hugo installed, you can start editing the files in the `content`
folder.

### Run local server to check changes
```
hugo server
```

## Update CLI docs (optional)

Run the create-cli-docs command (for Lightstreams developers only):
```
./bin/create-cli-docs
```

### Publish & deploy changes

```
./bin/deploy-gh-pages
```

## Updating content manually

Change the necessary content in `content` folder, then:

```
cd public
git reset --hard origin/master
cd .. # docs project folder
hugo
cd public
git add .
git commit -m "rebuilding site `date +"%Y-%m-%d %T"`"
git push origin master
cd ..
git add .
git commit -m "Updates content + public submodule ref"
git push origin master
```
