---
icon: code
title: Hacks
image: https://raw.githubusercontent.com/blockyfish-client/Assets/main/blockyfishclientbanner.png
---
# Hack scripts
These scripts are for people who cannot use the Blockyfish Client for any reasons. 

## Enabling Commands!
:::left-img
1. Go to [beta.deeeep.io](https://beta.deeeep.io)  

2. Open DevTools (yes that's what it's called) by using ctrl/cmd + shift + I (that's an i not an L)  

3. At the top, go to the sources tab  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/3.png)  
 
4. Find the index.js file in beta.deeeep.io/assets/index.xxxxx.js  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/4.png)  

5. Look towards the bottom and click the pretty-print button  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/5_1.png)  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/5_2.png)  
!!!info Note
Now you will see 50080-ish lines of code, don't be scared  
!!!

6. Use the "find" function (ctrl/cmd + F) and find "constructor"  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/6.png)  

7. Go to the very last one, 121/121. If there are more than 121, go to the last one, don't go to the 121st one. It should be at line 41672 or somewhere around there give or take 5000 - 15000 lines.  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/7.png)  


8. Now click on any one of these line numbers. You can pick any line as long as they are within the constructor.   
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/8_1.png)  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/8_2.png)  

9. Now you will see this. It may look a bit different depending on the line you clicked on. But the line number should turn blue.  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/9.png)  

10. If you look to the right, you will see that this new interesting thing that makes no sense has appeared  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/10_1.png)  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/10_2.png)  

## Getting the Commands to Work!
11. Now that you have the breakpoint thing added, press the play button. Yes, the depio play button. Do not touch random things in DevTools.  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/11.png)
12. Now it will get stuck here with a message saying "Pause in debugger"  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/12.png)
13. In DevTools, go to the Console tab  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/13.png)
14. Put this in the console:
!!!warning Important
When changing gamemodes or loading a new map (e.g. PD/1v1), you need to run `window.game = this` again when you get to the debugger pause
!!!
```
window.game = this
```
15. You will get a response ~~it will deez nutz you~~  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/15.png)
16. Press the unpause button in the debug thing that popped-up in step 12. Note that it's the blue button, I REPEAT THE BLUE BUTTON!  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/16.png)
17. Now there will be 2 outcomes:  
  a. It shows the evo menu, in this case, proceed on to step 18  
  b. It returns you to the menu page. Press play again. This time, simply unpause the debugger. DO NOT PASTE THE COMMAND IN STEP 14 INTO THE CONSOLE AGAIN!
18. Choose an animal *\*duh\**  
-![](https://raw.githubusercontent.com/ThePiGuy3141/DeeeepioHackedClient/main/img/18.png)

## Different hack scripts
19. There are various hacks you can use, I will list them below. Paste these commands into the console (the thing you used in step 14)
### **Transparent terrain**
#### **Ground:**
```
setInterval(function () {
for (let i = 0; i < game.currentScene.terrainManager.terrains.length; i++) {
    game.currentScene.terrainManager.terrains[i].alpha = 0.5;
}
}, 10);
```
#### **Ceiling (the thing that turns transparent when you go through them)**
```
setInterval(function () {
game.currentScene.ceilingsContainer.alpha = 0.3
}, 10);
```
### **Infinite zoom**
```
setInterval(function () {
game.viewport.clampZoom({
    minWidth: 0,
    maxWidth: 1e7,
})
}, 10);
```
### **Anti-ink and anti-darkness (in deep)**
```
setInterval(function () {
    game.currentScene.terrainManager.shadow.setShadowSize(1000000)
}, 10);
```
### **Anti-megamouth (no more flash-bangs)**
```
game.currentScene.toggleFlash = function() {console.log('xd you got flash-banged but a hack saved you')}
```
### **Visible hiding animals (buggy)**
```
setInterval(function () {
game.currentScene.myAnimal.handleHide = (function(){
game.currentScene.myAnimal.inner.alpha = 0.6
game.currentScene.myAnimal.sprite.scale.x = game.currentScene.myAnimal.origScale.x * 0.7
game.currentScene.myAnimal.sprite.scale.y = game.currentScene.myAnimal.origScale.y * 0.7
})
for (let i = 0; i < game.currentScene.entityManager.animalsList.length; i++) {
game.currentScene.entityManager.animalsList[i].handleHide = (function(){
game.currentScene.entityManager.animalsList[i].inner.alpha = 0.6
game.currentScene.entityManager.animalsList[i].sprite.scale.x = game.currentScene.entityManager.animalsList[i].origScale.x * 0.7
game.currentScene.entityManager.animalsList[i].sprite.scale.y = game.currentScene.entityManager.animalsList[i].origScale.y * 0.7
})
}
}, 10);
```

### **Super thresher**
!!!
Hold down control + shift then click. You need two boost to do this. 
!!!
```
window.addEventListener("click",
    function(e) {
        if (e.ctrlKey) {
            if (e.shiftKey && game.currentScene.myAnimal._visibleFishLevel == 101) {
                game.inputManager.handleLongPress(5000)
            }
        }
    },
false);
```

### **All in one hacks**
```
game.currentScene.toggleFlash = function() {console.log('xd you got flash-banged but a hack saved you')}
setInterval(function () {
for (let i = 0; i < game.currentScene.terrainManager.terrains.length; i++) {
    game.currentScene.terrainManager.terrains[i].alpha = 0.5;
}
game.currentScene.ceilingsContainer.alpha = 0.3
game.viewport.clampZoom({
    minWidth: 0,
    maxWidth: 1e7,
})
game.currentScene.terrainManager.shadow.setShadowSize(1000000)
game.currentScene.myAnimal.handleHide = (function(){
game.currentScene.myAnimal.inner.alpha = 0.6
game.currentScene.myAnimal.sprite.scale.x = game.currentScene.myAnimal.origScale.x * 0.7
game.currentScene.myAnimal.sprite.scale.y = game.currentScene.myAnimal.origScale.y * 0.7
})
for (let i = 0; i < game.currentScene.entityManager.animalsList.length; i++) {
game.currentScene.entityManager.animalsList[i].handleHide = (function(){
game.currentScene.entityManager.animalsList[i].inner.alpha = 0.6
game.currentScene.entityManager.animalsList[i].sprite.scale.x = game.currentScene.entityManager.animalsList[i].origScale.x * 0.7
game.currentScene.entityManager.animalsList[i].sprite.scale.y = game.currentScene.entityManager.animalsList[i].origScale.y * 0.7
})
}
}, 10);
```

## Multiboxing script
If you need assistance, message me on Discord
[-![](https://dcbadge.vercel.app/api/shield/777662985165864980?style=for-the-badge&theme=discord-inverted)](https://discord.com)

!!! Note
NOTE: You need to do [Enabling Commands](#enabling-commands) on all your tabs, ghost and animals. 
!!!

For the ghost (getting ID)
```
game.currentScene.myAnimal.id
```


For the animals following ghost
```
mapeditor = document.querySelector('#canvas-container > canvas')
ghostTarget = *targetIdHere*
click0 = game.currentScene.entityManager.getEntity(ghostTarget).relatedObjects.children[2].speedMultiplierDisplay.visible;
setInterval(function () {
	click1 = game.currentScene.entityManager.getEntity(ghostTarget).relatedObjects.children[2].speedMultiplierDisplay.visible;
	c = {"x": innerWidth/2 + game.currentScene.entityManager.getEntity(ghostTarget).position.x - game.currentScene.myAnimal.position._x, "y": innerHeight/2 + game.currentScene.entityManager.getEntity(ghostTarget).position.y - game.currentScene.myAnimal.position._y}
	mapeditor.dispatchEvent(new MouseEvent("pointermove", {clientX:c.x, clientY:c.y}))
	if (click0 != click1) {
		click0 = click1
		if (click1) {
			game.inputManager.spaceKeyDown()
		}
		else {
			game.inputManager.spaceKeyUp()
		}
	}
}, 200);
```
:::