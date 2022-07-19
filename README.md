# Instructions from this repo
1. Clone repo
2. Run `npm Install`
3. Run npx cordova prepare electron
(To reset run `npm run init`)

# Instructions from scratch

## Create the app and add plugin
>`npx cordova create myApp org.apache.cordova.myApp myApp`  
`cd myapp`  
`npm install cordova --save-dev`  
`npx cordova plugin add cordova-plugin-device`  
`npx cordova platform add electron`  

## Reset like it would get it from source control in the .gitignore
>`npx rimraf ./plugins && npx rimraf ./platforms`

## Prepare the platform like in build servers
>`npx cordova prepare electron`

## Output
```
PS C:\dev\testusecase\myApp> npx cordova prepare electron
npx: installed 495 in 39.075s
Discovered platform "electron". Adding it to the project
Using cordova-fetch for cordova-electron@^3.1.0
Adding electron project...
Creating Cordova project for cordova-electron:
        Path: C:\dev\testusecase\myApp\platforms\electron
        Name: myApp
Discovered plugin "cordova-plugin-device". Adding it to the project
Installing "cordova-plugin-device" for electron
Error during processing of action! Attempting to revert...
Failed to install 'cordova-plugin-device': Error: Uh oh!
ENOENT: no such file or directory, open 'C:\dev\testusecase\myApp\platforms\electron\www\package.json'
    at Object.openSync (fs.js:497:3)
    at Object.readFileSync (fs.js:393:35)
    at Object.install (C:\dev\testusecase\myApp\node_modules\cordova-electron\lib\handler.js:131:44)    at C:\dev\testusecase\myApp\node_modules\cordova-electron\lib\Api.js:212:31
    at ActionStack.process (C:\dev\testusecase\myApp\node_modules\cordova-common\src\ActionStack.js:56:25)
    at Api.addPlugin (C:\dev\testusecase\myApp\node_modules\cordova-electron\lib\Api.js:132:24)     
    at handleInstall (C:\Users\m.hipper\AppData\Roaming\npm-cache\_npx\32496\node_modules\cordova\node_modules\cordova-lib\src\plugman\install.js:561:10)
    at C:\Users\m.hipper\AppData\Roaming\npm-cache\_npx\32496\node_modules\cordova\node_modules\cordova-lib\src\plugman\install.js:344:28
    at processTicksAndRejections (internal/process/task_queues.js:95:5)
Uh oh!
ENOENT: no such file or directory, open 'C:\dev\testusecase\myApp\platforms\electron\www\package.json'
Error: spawn C:\Windows\system32\cmd.exe ENOENT
    at Process.ChildProcess._handle.onexit (internal/child_process.js:274:19)
    at onErrorNT (internal/child_process.js:469:16)
    at processTicksAndRejections (internal/process/task_queues.js:82:21)
PS C:\dev\testusecase\myApp>
```


## Work around
Add in a `<hook src="before_plugin_install.js" type="before_plugin_install" />` config.xml hook with code to create a blank package.json.