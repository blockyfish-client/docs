---
label: Building
icon: package
order: 998
---
# Building the app
If you are familiar with Git and Node.js, you can try building the app yourself.

## Prerequisites
- [NodeJS](https://nodejs.org/en/download/)
- [Git](https://gitforwindows.org/)  

## Build
**Cloning the repo**  
Downloads all the necessary files for building. 
```
mkdir blockyfish-client
git clone https://github.com/blockyfish-client/Desktop-Client.git blockyfish-client
cd blockyfish-client
```  

**Install node modules**  
Installs all dependencies. 
```
npm i
```
**Run the app**  
If you want to experiment with the code or you just want to run the app once, use this. 
```
npm run start
```
**Build an installer**  
If you want to make a fork and distribute your own variation of the client, you can use this to create installation packages for users. 
```
npm run make-win
npm run pack-win
```