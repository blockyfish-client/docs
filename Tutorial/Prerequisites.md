---
order: 100
---

# Prerequisites

The goal of this tutorial is to guide you through the process of creating a plugin for Blockyfish client.

This tutorial assumes that you have a considerable amount of knowledge in the inner-workings of the [Deeeep.io game client](https://beta.deeeep.io). If you are not familiar with it, please consider doing some background exploration of the `game.currentScene`.

All Blockyfish plugins are made with JavaScript, so it is important that you are familiar with the language. If you need to do some background reading, it is recommended to use [Mozilla's Javascript documentations](https://developer.mozilla.org/en-US/docs/Learn/JavaScript).

## Required tools

### Code editor

You will need a text editor in order to write code. It is recommended that you use Microsoft's [Visual Studio Code](https://code.visualstudio.com/)

### Command line (CLI)

Occasionally, you will need to use CLIs. Please familiarize yourself with your system's default terminal. Visual Studio Code has an integrated terminal, which you can also use.

### Node.js and npm

To test your plugins, you will need to run Blockyfish client from its source code. Since it is built with Electron.js, you will need to have [Node.js](https://nodejs.org/en/download/) and npm installed.

Check that Node.js and npm are installed correctly by running the following command:

```sh
node -v
npm -v
```

They should return a version number like so:
!!! Note
The version number returned may vary depending on what version of Node.js and npm you have installed.
!!!

```sh
$ node -v
# returns v20.10.0
$ npm -v
# returns 10.2.3
```

### Blockyfish client

In order to test and debug your plugins, it is recommended to run Blockyfish from source. You should also familiarize yourself with the process of loading external plugins in Blockyfish client.

#### Downloading

Start by cloning the GitHub repository.

```sh
git clone https://github.com/blockyfish-client/desktop-client
cd desktop-client
```

!!!warning Important!
Before continuing, please check to make sure that you have Node.js installed.
!!!
Install the required Node.js modules

```sh
npm install
```

#### Running Blockyfish client in debug mode

In debug mode, DevTools will be opened so you can use it for testing various things. Learn more about it [here](../testing-and-debugging/#loading-external-plugins)

```sh
npm run test
```
