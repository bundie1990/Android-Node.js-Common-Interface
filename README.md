# Introduction
- This framework is named Android/Node Common Interface, abbreviated ANCI
- Targets to let program designers write a JavaScript APP once
- And be able to use it on 
  + Android (under DroidScript framework)
  + Node.js enabled device (running a server, the APP at the client side)
  + Windows/Linux/MacOS by utilizing Electron
# File system structure
## Overview
- For a comprehensive view, please look at the Project_Structure.pptx or the demo images
## sdcard (/sdcard)
- Access by RELATIVE path in HTML files, but when using filesystem operations by anci.operations in JS files, use absolute path starting with /sdcard
- As to emulate the environment of Android system
- The uppermost folder that the cient side can access to protect server's code
+ napps folder: abbreviation of Node.js APPs, where your APPs are stored
  * /sdcard/napps/app_name on Node.js
  * the corresponding folder on Android is /sdcard/DroidScript/app_name
  * Call anci.GetAppPath() to access
+ nlib folder: abbreviation of Node.js libraries, the common lib for all APPs
  * this folder will be mapped under /sdcard/napps/app_name/nlib on Node.js
  * and copied to /sdcard/DroidScript/app_name/nlib on Android
  * Call anci.GetAppPath() to access
+ ndata folder: stores application data on the filesystem
  * this folder will remain accessed as /sdcard/ndata on both Android/Node.js
  * So use ABSOLUTE path to access it
## sdcard/napps/app_name/main.app
- A virtual path to evoke server-side generation of an APP's complete HTML
- the app_name 0 is the default app
- if the server was called w/o path, i.e http://xxx.xxx.x.x, default APP runs
  at http://xxx.xxx.x.x/sdcard/napps/0/main.app
- the APPs' complete HTML comprises
  + ~app_entry.html (/node-head.html)
  + xxx_api_anci.js (web_electron or droidscript)
  + query parameters (URL?para1=val_a&parameter2=val_b) as app.query
  + Code.js (/sdcard/napps/app_name/Code.js)
  + UI.html (/sdcard/napps/app_name/UI.html)