# Discord Rich Presence
Blockyfish Client comes with a Discord Rich Presence integration that allows your friends on Discord to see that you are playing the game. 

## Supported states
### Gamemodes
When showing status as playing gamemode, a button will be shown to let others join your lobby. 
- FFA
- TFFA
- PD
- 1v1

### Other
- Viewing `user`'s profile
- Browsing through the store
- Checking inventory
- Visiting the forums
- In the menus

## How it works
### Reporting gamemode
A background script on the game's page logs the text of the selected gamemode button. The script also checks to see whether the menu is visible to determine if the user is playing or if the game is paused. A script running in the Electron app intercepts that log message. It checks to see the gamemode and pause state to determine whether to show `Playing gamemode` or `In the menus`. 
```js Getting gamemode and play status
if (document.querySelector('div.home-page').style.display == 'none') {
    rpc_state = document.querySelector('.selected').innerText + "2"
}
else {
    rpc_state = document.querySelector('.selected').innerText + "0"
}
console.log("state: " + rpc_state)
```

### Other state checking stuff
Checks to see if the URL contains `/u/`. If it does, then remove all the `https://beta.deeeep.io/u/` and `?host=randomstring` stuff and then set the RPC status to the remaining string, which will be the username.

For other states, check to see if `forum`, `store`, and `inventory` are in the URL and set the RPC status accordingly. 

If the menu is visible, show that the user is in the menu. Otherwise, show that they're playing a certain gamemode. 
```js Checking for other RPC states
var currentUrl = win.webContents.getURL()
if (matches(currentUrl, "/u/")) {
    var detailText = 'Viewing ' + currentUrl.replace("https://beta.deeeep.io/u/", "").replace(/\?host=....../i, "") + "'s profile"
    var labelText = ''
    if (currentUrl.replace("https://beta.deeeep.io/u/", "").replace(/\?host=....../i, "") == 'ItsGrandPi') {
        insertClientOwnerBadge()
    }
}
else if (matches(currentUrl, "/forum/")) {
    var detailText = "Visiting the forums"
    var labelText = ''
}
else if (matches(currentUrl, "/store/")) {
    var detailText = "Browsing through the store"
    var labelText = ''
}
else if (matches(currentUrl, "/inventory/")) {
    var detailText = "Checking inventory"
    var labelText = ''
}
else if (menu == '0') {
    var detailText = 'In the menus'
    var labelText = ''
}
else {
    var detailText = "Playing " + mode
    var labelText = 'Join game'
}
```