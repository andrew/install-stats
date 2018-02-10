# install-stats

Record install information for your npm packages in Google Analytics

# Setup

First, if you haven't already got one, setup a Google Analytics account: https://analytics.google.com

Create a new property and copy the tracking id, it should look like: `UA-XXXXXX-XX`

Add `install-stats` as a dependency of your module's package.json:

```json
"dependencies": {
  "install-stats": "1.x"
},
```

Then add the install script to the package.json file, including your Google Analytics property tracking id:

```json
"scripts": {
  "install": "TID=UA-XXXXXX-XX node_modules/.bin/install-stats"
},
```

Then publish a new version to npm and install data will begin to show up in Google Analytics under the `Event` sections.

# License

[LGPL-3.0](LICENSE) © 2018 Andrew Nesbitt.
