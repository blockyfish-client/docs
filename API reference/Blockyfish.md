---
order: 100
---

# blockyfish

## Events

### death

Fires when the player dies.

Useful for modifying the death screen.

### first-game-load

Fires in the first time that the game object is loaded. Subsequent loads will trigger `game-load`.

### forums-open

Fires when the player opens the forums.

Useful for modifying theme or behavior of the forums.

### game-load

Fires everytime the game object is loaded except for the first time. On the first time that the game object is loaded, the `first-game-load` event will be fired instead.

### play-button-click

Fires everytime the player clicks on the Play button. Always fires, regardless of whether the game object has already been loaded.

### settings-open

Fires when the player opens the settings.

Useful for modifying the settings page layout or elements.

## Methods

### addEventListener

Adds an event listener for an event

```js
blockyfish.addEventListener("game-load", () => {
    // do stuff...
})
```

### emit

Used internally by blockyfish client to dispatch events

### formBytePacket

Creates a byte packet

### formMovePacket

Creates a movement packet

### getVersion

Get the current client version in a human-readable format

### getVersionNumber

Get the current client version as a number

### removeEventListener

Removes an event listener for an event

### sendChat

Sends a message in the chat
