---
order: 97
---

# Testing and debugging

When your plugin does not work as expected, you may need to debug it. The following instructions will explain how you can do so.

First, you should run Blockyfish client in debug mode.

Make sure you have already downloaded the source code, if not, please see [here](/tutorial/prerequisites#blockyfish-client).

You can do that by first opening the directory that contains the downloaded Blockyfish client source code and running the following:

```sh
npm run test
```

## Loading external plugins

Normally, Blockyfish only allows you to use the provided plugins. However, you can also load your own plugins by manually putting the plugin file into the plugins folder, which is generally located at `%AppData%\Blockyfish Client\plugins\`.

You can also easily locate the plugins folder by doing the following:

1. Start Blockyfish client.
2. Open the plugins page by clicking on the `Plugins` button located towards the right.
3. Click the letter `g` on the plugins modal title.
4. A confirmation dialog will pop-up, press `Continue`.
5. A file explorer window will be opened, showing the plugins folder.
6. Move or copy your plugin into the folder and restart Blockyfish client to apply changes.
    !!! Note
    You may need to enable the plugin after loading it in
    !!!
