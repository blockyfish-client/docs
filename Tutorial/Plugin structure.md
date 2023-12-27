---
order: 99
---

# Plugin structure

Blockyfish client plugins have these main variables that **must** be exported:

- **name**: Display name of the plugin
- **id**: A constant string that is used to identify plugins. This should never change. Generally formatted like so: `plugins.<author>.<pluginname>`
- **author**: Name of the plugin creator
- **version**: Human readable version string
- **versionNumber**: Integer representing the current version, newer versions of the plugin must have a higher version number than older versions
- **description**: String that describes the function of the plugin
- **script**: The JavaScript code of the plugin. This function executed when the plugin is loaded.

Here is an example plugin:

```js
const name = "Dummy plugin";
const id = "plugins.anon.dummyplugin";
const author = "Anon";
const version = "1.0.0";
const versionNumber = 1000;
const description = "This plugin does nothing";
const script = () => {
    console.log("Hello World!")
};

module.exports = { name, id, author, version, versionNumber, description, script };
```
