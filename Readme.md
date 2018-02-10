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

# Notes

- IP addresses are anonymized: https://support.google.com/analytics/answer/2763052?hl=en
- Doesn't currently track installs with yarn

# Setup

First, if you haven't already got one, setup a Google Analytics account: https://analytics.google.com

Create a new property and copy the tracking id, it should look like: `UA-XXXXXX-XX`

Next you need to create four custom dimensions within the google analytics property settings, the order is important:

| Index | Name             | Scope |
|-------|------------------|-------|
| 1     | node version     | Hit   |
| 2     | npm version      | Hit   |
| 3     | operating system | Hit   |
| 4     | architecture     | Hit   |

More detailed instructions here: https://support.google.com/analytics/answer/2709829

_note: Due to a [bug](https://github.com/npm/npm/issues/17316) in npm@5 this can't be reliably loaded as a dependency so the script needs to be included within your module for now._

Copy and paste the contents of [`index.js`](index.js) into `scripts/install-stats.js` within your module.

Then add the postinstall script to the package.json file, including your Google Analytics property tracking id:

```json
"scripts": {
  "postinstall": "TID=UA-XXXXXX-XX script/install-stats.js"
},
```

Then publish a new version to npm and install data will begin to show up in Google Analytics under the `Event` sections.

# Exporting data

This package does not provide any interface for exporting data directly but Google Analytics has an advanced API for generate reports that you can use to export data: https://developers.google.com/analytics/devguides/reporting/core/v4/quickstart/web-js

Installs are stored in Google Analytics as events (rather than traditional pageviews) with custom dimensions for each attribute of the system it was install in.

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
