# install-stats

Record install information for your npm packages in Google Analytics.

install-stats helps you find out:

- installed versions of your package
- which versions of node.js are used to install your packages
- which versions of npm are used to install your packages
- which operating systems your packages installed on
- which architectures (x86, x64 etc) your packages installed on
- other names your package may be published under
- plus most of the features of [Google Analytics](https://analytics.google.com)

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

# Exporting data

This package does not provide any interface for exporting data directly but Google Analytics has an advanced API for generate reports that you can use to export data: https://developers.google.com/analytics/devguides/reporting/core/v4/quickstart/web-js

# Disabling

To disable stats tracking with the `--ignore-scripts` flag in npm, for a one time install:

```shell
npm install --ignore-scripts
```

Or permanently disable scripts with the following command:

```shell
npm config set ignore-scripts true
```

# License

[LGPL-3.0](LICENSE) © 2018 Andrew Nesbitt.
