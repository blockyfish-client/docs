---
icon: chevron-right
order: 995
title: Forum stuff
image: https://raw.githubusercontent.com/blockyfish-client/Assets/main/blockyfishclientbanner.png
---
# Forum Notification Badges
When you have a forum notification, Blockyfish Client will display it as a badge on the taskbar icon if the app is running. 

## How it works
### Getting notification count
Uses the forum button notification badge and gets the value of the badge. If the badge doesn't exist, then assume there are 0 notifications. After getting the notification count, check to see if the count has changed. If it has, then log a message in the console that will be intercepted by the Electron app process. 
```js
if (document.querySelector('span.forum-notifications-badge') != null) {
    notif_count = document.querySelector('span.forum-notifications-badge').innerText
}
else {
    notif_count = 0
}
if (notif_count != notif_count_old) {
    console.log("notifs: " + notif_count)
    notif_count_old = notif_count
}
```

### Displaying notification badges on the taskbar icon
Intercepts the console message. If it matches the identifier `notifs`, then find the length of the string. 

If the length is more than 10 or more, then the notification count is a 2-digit number and is therefore greater than 9. In this case, the badge would be set to [!badge variant="danger" text="9+"] 

If the length is 9, then the notification count is a single-digit number and the exact number can be shown on the taskbar icon badge. Taskbar badges for Electron apps are set with image files. To set the right number badge, the last digit of the string is taken and joined with the directory to the number badge image. 
```js
if (matches(msg, "notifs:")) {
    if (msg.length < 10) {
        const msg_num = msg.charAt(msg.length - 1);
        if (msg_num != 0) {
            win.setOverlayIcon(path.join(__dirname, 'img/' + msg_num + '.png'), 'Over ' + msg_num + ' notifications')
        }
        else {
            win.setOverlayIcon(null, '')
        }
    }
    else {
        win.setOverlayIcon(path.join(__dirname, 'img/9_plus.png'), 'Over 9 notifications')
    }
}
```

# Forum auto-loading
When you scroll down, posts will keep loading automatically so you don't have to press the `load more` button. 

## How it works
When the load more button scrolls into view, the script automatically presses it. 
```js
function isInViewport(e) {
    const rect = e.getBoundingClientRect();
    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <= (window.innerWidth || document.documentElement.clientWidth)
    );
}
document.querySelector('#app > div.ui > div > div.el-row.header.justify-between.flex-nowrap > div:nth-child(2) > div > div:nth-child(3) > button').addEventListene("click", () => {
    document.querySelector('#app > div.vfm.vfm--inset.vfm--fixed.modal > div.vfm__container.vfm--absolute.vfm--inset.vfm--outline-none.modal-container > div > div > div').addEventListener("scroll", function() {
        if (isInViewport(document.querySelector('#app > div.vfm.vfm--inset.vfm--fixed.modal > div.vfm__container.vfm--absolute.vfm--inset.vfm--outline-none.modal-container > div > div > div > div > div.footer > button'))) {
            document.querySelector('#app > div.vfm.vfm--inset.vfm--fixed.modal > div.vfm__container.vfm--absolute.vfm--inset.vfm--outline-none.modal-container > div > div > div > div > div.footer > button').click()
        }
    })
})
```