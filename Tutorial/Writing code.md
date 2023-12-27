---
order: 98
---

# Writing code

For this tutorial, we will be making a plugin that allows you to see through the ground and removes ink, darkness, and flashbang.

## Creating a plugin file

First, let's make a new JavaScript file. This tutorial will call it `esp.js` but you can name it anything you want. Start off with the dummy plugin template:

```js esp.js
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

Then, let's modify the dummy plugin template a little.

```js !#1-3,6 esp.js
const name = "ESP";
const id = "plugins.tutorial.esp";
const author = "Blockyfish tutorial";
const version = "1.0.0";
const versionNumber = 1000;
const description = "Allows you to see through the ground. Also removes ink, darkness, and flashbang.";
const script = () => {
    console.log("Hello World!")
};

module.exports = { name, id, author, version, versionNumber, description, script };
```

## Coding the plugin

Now, we need to actually write JavaScript code for the plugin.
!!!info Tip
In the following steps, only the code within `script` will be shown to save space. But keep in mind that it is not the whole plugin file.
!!!

Since everything we will be modifying here needs to modify the Deeeep.io game object, we need to detect when the game loads. Blockyfish has an event system that automatically fires when certain events occur.

The `first-game-load` event only fires when the game object is loaded for the first time.

The `game-load` event fires every time the game object is loaded except for the first time.

```js !#1-6 esp.js
blockyfish.addEventListener("first-game-load", () => {
    // code goes here
});
blockyfish.addEventListener("game-load", () => {
    // code goes here
});
```

### Removing flashbang, ink, and darkness

When the game loads, we need to disable function that creates the flashbang and darkness overlay. Ink uses the same function as darkness.

```js !#2-3 esp.js
blockyfish.addEventListener("first-game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};
});
blockyfish.addEventListener("game-load", () => {
    // code goes here
});
```

Sometimes, the animal can also spawn in a deep area, so we need to remove the darkness first before nullifying the function. Otherwise, the darkness overlay will be stuck there forever!

```js !#3 esp.js
blockyfish.addEventListener("first-game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};
});
blockyfish.addEventListener("game-load", () => {
    // code goes here
});
```

Now everything works perfectly... well, not exactly. The function will only run on the first game load. When the game object loads again, it will reassign the `toggleFlash` and `setShadowSize` functions. Therefore, we need to also copy the function over to the `game-load` event.

```js !#7-9 esp.js
blockyfish.addEventListener("first-game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};
});
blockyfish.addEventListener("game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};
});
```

### Seeing through terrain

First, let's change the z-order of the elements that we want to be shown on top of the terrain layer

```js !#6-11,18-23 esp.js
blockyfish.addEventListener("first-game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};

    game.currentScene.foodGlowContainer.zOrder = 996;
    game.currentScene.foodContainer.zOrder = 997;
    game.currentScene.namesLayer.zOrder = 998;
    game.currentScene.animalsContainer.zOrder = 999;
    game.currentScene.barsLayer.zOrder = 1000;
    game.currentScene.chatContainer.zOrder = 1001;
});
blockyfish.addEventListener("game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};

    game.currentScene.foodGlowContainer.zOrder = 996;
    game.currentScene.foodContainer.zOrder = 997;
    game.currentScene.namesLayer.zOrder = 998;
    game.currentScene.animalsContainer.zOrder = 999;
    game.currentScene.barsLayer.zOrder = 1000;
    game.currentScene.chatContainer.zOrder = 1001;
});
```

We also need to constantly reassign the alpha value of all ceilings (terrain "tunnels" that turn transparent when you go through them). Let's give it an alpha value of `0.3` so that it will be translucent.

```js !#13-17 esp.js
blockyfish.addEventListener("first-game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};

    game.currentScene.foodGlowContainer.zOrder = 996;
    game.currentScene.foodContainer.zOrder = 997;
    game.currentScene.namesLayer.zOrder = 998;
    game.currentScene.animalsContainer.zOrder = 999;
    game.currentScene.barsLayer.zOrder = 1000;
    game.currentScene.chatContainer.zOrder = 1001;

    setInterval(function () {
        try {
            game.currentScene.ceilingsContainer.alpha = 0.3;
        } catch {}
    }, 200);
});
blockyfish.addEventListener("game-load", () => {
    game.currentScene.toggleFlash = function () {};
    game.currentScene.terrainManager.shadow.setShadowSize(1000000);
    game.currentScene.terrainManager.shadow.setShadowSize = function () {};

    game.currentScene.foodGlowContainer.zOrder = 996;
    game.currentScene.foodContainer.zOrder = 997;
    game.currentScene.namesLayer.zOrder = 998;
    game.currentScene.animalsContainer.zOrder = 999;
    game.currentScene.barsLayer.zOrder = 1000;
    game.currentScene.chatContainer.zOrder = 1001;
});
```

And that's it! You've finished your first Blockyfish plugin. 🎉

!!!success Here is the full code for the plugin:

```js
const name = "ESP";
const id = "plugins.tutorial.esp";
const author = "Blockyfish tutorial";
const version = "1.0.0";
const versionNumber = 1000;
const description = "Allows you to see through the ground. Also removes ink, darkness, and flashbang.";
const script = () => {
    blockyfish.addEventListener("first-game-load", () => {
        game.currentScene.toggleFlash = function () {};
        game.currentScene.terrainManager.shadow.setShadowSize(1000000);
        game.currentScene.terrainManager.shadow.setShadowSize = function () {};
    
        game.currentScene.foodGlowContainer.zOrder = 996;
        game.currentScene.foodContainer.zOrder = 997;
        game.currentScene.namesLayer.zOrder = 998;
        game.currentScene.animalsContainer.zOrder = 999;
        game.currentScene.barsLayer.zOrder = 1000;
        game.currentScene.chatContainer.zOrder = 1001;
    
        setInterval(function () {
            try {
                game.currentScene.ceilingsContainer.alpha = 0.3;
            } catch {}
        }, 200);
    });
    blockyfish.addEventListener("game-load", () => {
        game.currentScene.toggleFlash = function () {};
        game.currentScene.terrainManager.shadow.setShadowSize(1000000);
        game.currentScene.terrainManager.shadow.setShadowSize = function () {};
    
        game.currentScene.foodGlowContainer.zOrder = 996;
        game.currentScene.foodContainer.zOrder = 997;
        game.currentScene.namesLayer.zOrder = 998;
        game.currentScene.animalsContainer.zOrder = 999;
        game.currentScene.barsLayer.zOrder = 1000;
        game.currentScene.chatContainer.zOrder = 1001;
    });
};

module.exports = { name, id, author, version, versionNumber, description, script };
```

!!!
