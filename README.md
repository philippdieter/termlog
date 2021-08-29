# Termlog
Bring browser console to your terminal

### What it does
termlog send the browser console log to your terminal.

It also comes with a __nodejs__ REPL so you can do some basic draft code

### When to use it
- While you developing your front-end app and you have to switch back and forth between IDE and browser.
- When you want to test app on mobile need to check log. (See [Debug on mobile](#debug-on-mobile))

# How to use it?
There are 2 ways and it depends on your preferences

## Recommended way
1. Install the `termlog` binary : `npm install --save-dev termlog` ( you also can install globally with `npm install -g termlog` )
2. Start server `npx termlog` or `termlog` if you install globally
3. Go to the entry file of your project (I.e: app.jsx for React or main.js for Vue)
4. Insert these two lines:
```
import termlog from "termlog"
termlog()
```
4. You should now see log being streamed to your terminal

__Note__: with this approach you might want to remove two lines above in production. 

By default termlog will __not__ run if it detects production mode using `NODE_ENV`, but you shouldn't rely on that.

## I don't want to add dependencies to my project
1. Install the `termlog` binary : `npm install -g termlog`
2. Start server `termlog`
3. Go to your browser and open the console window
4. Copy code inside [index.js](index.js) file __without__ the last export line into console
5. Enter `termlog()` into console
6. You should now see log being streamed to your terminal

__Note__: with this approach you have to do all steps 3-6 every-time you refresh your browser tab.

## Advanced options
With `tconsole` command:
- `--out path`: Save log to file
- `--port port`: Change server port
- `--addr addr`: Change server address
- `--show levels`:  Select log levels to display (info | warning | error | debug). Multiple levels are seperated by `,`
> use `.show levels` while the server running to select again
  

With `tconsole` package:

`tconsole({
host: "localhost",
port: 3456
})`

## Debug on mobile
To be able to stream log from your app running on mobile you need to :
- Start term log with `0.0.0.0` by running `npx termlog --addr 0.0.0.0`
- Find your private IP address
  -  MacOS: run `ipconfig getifaddr en0` if you're on wifi and 
  -  Linux: run `hostname -I`
  -  Windows: run `ipconfig` and find in the printed result. It should be under `192.168.x.x`
- Inside your project init tconfig with: `termlog({host: "YOUR_PRIVATE_IP})`

## How it works
Tconsole have 2 components:
- [server.js](cli.js) - a websocket server to receive log from browser and display it
- [index.js](index.js) - tconsole package to import in your front end app. This package will override the default behavior of console object and send log to the server

## Future release
- [ ] Install using `<script/>` tag
- [ ] (Maybe) An extension to start termlog on browser so we don't have to install dependencies
- [ ] (If possible) Browser console REPL instead of nodejs REPL
