---
order: 96
---

# Best practices

The following are some recommendations to consider when making plugins.

## Use try-catch

When writing code that may return errors under certain circumstances (e.g. when referencing the game object), it is recommended to use a try-catch statement to avoid flooding the console with errors.

+++:icon-check: Correct

```js
setInterval(() => {
    try {
        game.currentScene.myAnimal.alpha = 1;
    } catch {}
}, 100)
```

+++:icon-x: Incorrect

```js
setInterval(() => {
    game.currentScene.myAnimal.alpha = 1;
}, 100)
```

!!!danger
This code is not good because the `game` object may become undefined if the user is not connected to a server.
!!!
+++

## Avoid using setInterval to detect events

As much as possible, try to use event listeners. Below is an example of detecting when the game object is initialized:

+++:icon-check: Correct

```js
blockyfish.addEventListener("first-game-load", () => {
    console.log("Game object initialized!");
});
```

+++:icon-x: Incorrect

```js
var inter = setInterval(() => {
    if (typeof window.game != "undefined") {
        clearInterval(inter);
        console.log("Game object initialized!");
    }
}, 5);
```

!!!danger
This code is not good because it is more resource demanding. This is because the code has to be called every 5ms to check if the game object is defined.
!!!
+++

## Check for input boxes when registering keybinds

When using `keydown` or `keypress` events to register keybind actions, check to make sure that the chat box or any other UI elements that may require typing is not visible. Otherwise, typing something may accidentally trigger the keybind.

+++:icon-check: Correct

```js
window.addEventListener("keydown", (e) => {
    if (
        e.key == "P" &&
        document.querySelector("#app > div.modals-container > div") == null &&
        document.querySelector("#app > div.ui > div").style.display == "none" &&
        document.activeElement.localName != "input"
    ) {
        doStuff();
    }
});
```

+++:icon-x: Incorrect

```js
window.addEventListener("keydown", (e) => {
    if (e.key == "P") {
        doStuff();
    }
});
```

!!!danger
This code is not good because it may be triggered when the user is typing.
!!!
+++
