---
icon: chevron-right
order: 996
title: Updater
image: https://raw.githubusercontent.com/blockyfish-client/Assets/main/blockyfishclientbanner.png
---
# Update Checker
Blockyfish Client has an automatic update checker that can notify you about available updates and download updates right from within the client. 

## How it works
### Making the updater button
The menu item is built by cloning one of the existing buttons and then modifying its icon, actions, and color. 
```js
const update_parent = document.querySelector('#app > div.ui > div > div.el-row.header.justify-between.flex-nowrap > div:nth-child(2) > div > div:nth-child(5)').cloneNode(true);
social_class.appendChild(update_parent);
update_parent.classList.add('update-div')
const update = document.querySelector('div.update-div > button')
const update_logo = document.querySelector('div.update-div > button > span > svg')
update.classList.remove("indigo")
update.classList.add("green", "update", "updater-close")
update_logo.outerHTML = '<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-clockwise" viewBox="0 0 16 16"><path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"/><path d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"/></svg>'
const update_notif_div = document.createElement('div')
update.appendChild(update_notif_div)
update_notif_div.outerHTML = '<div id="update-notif" style="width: 10px;height: 10px;position: absolute;background: #f00;right: -1px;bottom: -4px;border-radius: 10px; display:none;"></div>'
```

### Building the updater UI
Builds a box in the style of Deeeep.io v4 and adds stuff to it. 
+++JS
```js
const updater_style = document.createElement('style')
document.querySelector('head').appendChild(updater_style)
updater_style.innerHTML = //see the css tab
const updater_div = document.createElement('div')
document.getElementById('app').appendChild(updater_div)
updater_div.outerHTML = //see the Updater container tab
const updaterMain = document.getElementById("updater-main")
const updaterBox = document.createElement("div")
updaterMain.appendChild(updaterBox)
updaterBox.outerHTML = //see the Updater contents tab
const updateButton = document.getElementById("updater-load")
const updateImg = document.getElementById("updater-icon")
const updateText = document.getElementById("updater-text")
const updateDownloadButton = document.getElementById("updater-download")
const updateAvailableDiv = document.getElementById("update-available")
const updateAvailableText = document.getElementById("update-available-text")
const updaterCloses = document.getElementsByClassName("updater-close")
const updaterModal = document.getElementById("updater-modal")
updaterModal.classList.toggle("updater-hidden")
```
+++CSS
```css
.button{
    display:inline-flex;
    justify-content:center;
    align-items:center;
    line-height:1;
    height:32px;
    white-space:nowrap;
    cursor:pointer;
    text-align:center;
    box-sizing:border-box;
    outline:0;
    transition:.1s;
    -webkit-user-select:none;
    -moz-user-select:none;
    -ms-user-select:none;
    user-select:none;
    vertical-align:middle;
    -webkit-appearance:none;
    min-height:2.5rem;
    border-radius:.25rem;
    padding:.75rem 1.25rem;
    font-size:.875rem
}
.box-x-close{
    position:absolute;
    top:.3rem;
    right:.5rem
}
.updater-green{
    background-color:#10b981;
    border-color:#059669
}
.updater-green:hover{
    background-color:#059669;
    border-color:#047857
}
.updater-blue{
    background-color:#3b82f6;
    border-color:#2563eb
}
.updater-blue:hover{
    background-color:#2563eb;
    border-color:#1d4ed8
}
.updater-black:hover,.updater-disabled{
    background-color:#4b5563;
    border-color:#374151
}
.updater-disabled{
    color:#9ca3af;
    pointer-events:none
}
.updater-black{
    background-color:#6b7280;
    border-color:#4b5563
}
body .updater-button{
    border-bottom-width:4px;
    border-radius:1rem
}
.updater-box.active{
    outline:white solid 2px;
    filter:brightness(100%)
}
.updater-modal{
    background-color:#1f2937;
    border:2px solid #374151;
    border-radius:.75rem;
    width:300px
}
@media screen and (min-width:768px){
    .updater-modal{
        background-color:#1f2937;
        border:2px solid #374151;
        border-radius:.75rem;
        width:400px
    }
}
.updater-core{
    top:5px;
    right:5px;
    border:1px solid #fff;
    border-radius:25px;
    font-size:14px
}
#updater-main{
    justify-content:center;
    flex-wrap:wrap;
    width:88%;
    margin:auto;
    gap:15px;
    flex-direction:column;
    align-items:center
}
.updater-hidden{
    opacity:0;
    pointer-events:none
}
#updater-modal{
    transition:opacity .2s
}
#update-available{
    margin:10px;
    width:88%;
    background:#fff2;
    border-radius:10px;
    display:flex;
    flex-direction:row;
    align-items:center;
    padding:10px;
    justify-content:space-between
}
```
+++Updater container
```html
<div style="z-index: 100;" class="w-screen h-screen absolute" id="updater-modal">
   <div style="background-color: rgba(0,0,0,.5);" class="w-full h-full absolute"></div>
   <div class="w-full h-full absolute flex justify-center items-center">
      <div class="flex flex-col updater-modal relative">
         <div style="font-size: 1.3rem" class="text-center py-2">Updater</div>
         <button class="updater-close box-x-close">
            <svg width="1.125em" height="1.125em" viewBox="0 0 24 24" class="svg-icon" color="gray" style="--sx:1; --sy:1; --r:0deg;">
               <path d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z" fill="currentColor"></path>
            </svg>
         </button>
         <div style="flex: 1;" class="text-center">
            <div class="p-4 flex" id="updater-main"></div>
         </div>
         <div class="text-center py-4">
            <div id="updater-load" class="button updater-button updater-green" style="margin-right: 10px;">Check for Updates</div>
            <div class="button updater-button updater-black updater-close">Close</div>
         </div>
      </div>
   </div>
</div>
```
+++Updater contents
```html
<div style="display:none" id="update-available">
   <p id="update-available-text">Update available</p>
   <div id="updater-download" class="button updater-button updater-blue">Install</div>
</div>
<p id="updater-text">No updates available</p>
<svg id="updater-icon" xmlns="http://www.w3.org/2000/svg" width="50" height="50" fill="#374151" class="bi bi-arrow-clockwise" viewBox="0 0 16 16">
   <path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"></path>
   <path d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"></path>
</svg>
```
+++

### Making the buttons open/close the updater
Whenever the button is clicked, toggle a class that hides the updater modal. 
```js
function resetModal() {
    updateText.style.display = 'block'
    updateImg.style.display = 'block'
    updateAvailableDiv.style.display = 'none'
    updateDownloadButton.classList.remove('updater-disabled')
}
for (const updaterClose of updaterCloses) {
  updaterClose.addEventListener("click", () => {
    updaterModal.classList.toggle("updater-hidden")
    updateText.innerText = 'No updates available'
  })
}
```

### Spinny update icon!
Everyone **loves** spinny things so when they click the `Check for Updates` button, they will see the arrow spin. The spin is animated using CSS transitions. 
```js
async function spinUpdateIcon() {
    setTimeout(function() {
        updateImg.style.transition = '3s transform ease-in-out'
        updateImg.style.transform = 'rotateZ(1440deg)'
        setTimeout(function() {
            updateImg.style.transition = 'none'
            updateImg.style.transform = 'rotateZ(0deg)'
        }, 3000)
    }, 100)
}
```

### Fetching updates from GitHub
Updates are uploaded as releases on GitHub so we can use GitHub's API to find the latest version and compare it with the current client version. 
```js
async function getUpdates() {
    updateText.innerText = 'Checking for updates...'
    //getting JSON data from GitHub API
    let url_json = await (await (fetch('https://api.github.com/repos/blockyfish-client/desktop-client/releases/latest'))).json();
    var download_url = url_json.assets[0].browser_download_url
    var download_ver = url_json.tag_name
    //change v1.2.3 to 123 so we can compare them as integers instead of strings
    var ver_num = download_ver.replace("v", "").replace(".", "").replace(".", "")
    setTimeout(function() {
        //if the returned version number is greater than the current version number, then prompt user to download
        if (ver_num > ` + version_num + `) {
            updateText.style.display = 'none'
            updateImg.style.display = 'none'
            updateAvailableDiv.style.display = 'flex'
            updateAvailableText.outerHTML = '<p id="download-percent" style="text-align: left;">Update available<br><span style="color: #aaa">` + version_code + ` -&gt; ' + download_ver + '</span></p>'
            downloadPercentText = document.getElementById('download-percent')
            document.getElementById('update-notif').style.display = 'block'
            //disable the check for updates button when the user clicks it
            updateDownloadButton.addEventListener("click", () => {
                if (updateDownloadButton.disabled != true) {
                    console.log("request_download: " + download_url)
                    updateDownloadButton.classList.add('updater-disabled')
                    updateButton.classList.add('updater-disabled')
                }
            })
        }
        //otherwise, change text back to original
        else {
            updateText.innerText = 'No updates available'
        }
    }, 2500)
}
```

### Automatic update check
To check for updates automatically, a script is set to run once every 60 seconds and get any updates from the server. 
```js
setInterval(function() {
    spinUpdateIcon()
    getUpdates()
}, 60000)
```