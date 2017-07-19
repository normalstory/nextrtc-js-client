# NextRTC JavaScript client
If you want to use `nextrtc-js-client` you have to add to your code following .js files:
- adapter.js
- nextRTC.js

Both files are available in project nextrtc-js-client. Adapter is external resource taken from [here](https://webrtc.github.io/adapter/adapter-latest.js), so if you want to use newest version you should take it direct from [this](https://github.com/webrtc/adapter) project.

NextRTC js client constructor requires:

* **wsURL** which should points to your endpoint `{ws/wss}://{host}:{port}/{applicationName}/{endpointGivenInAnnotation}`
endpointGivenInAnnotation e.g. – @ServerEndpoint(value = “/signaling” …)
* **mediaConfig** are passed straight to adapter, so more information about parametres you can find in webrtc/adapter documentation.
* **peerConfig** are also described in [webrtc/adapter](https://github.com/webrtc/adapter) project.

Example is shown below and it’s also available in [nextrtc-videochat-example](https://github.com/mslosarz/nextrtc-example-videochat)

```js
new NextRTC({
    wsURL : 'wss://examples.nextrtc.org/videochat/signaling',
    mediaConfig : {
        video : true,
        audio : true,
    },
    peerConfig : {
        'iceServers' : [ {
            url : "stun:stun.l.google.com:19302"
        }]
    }
});
```

## How to use nextrtc-js-client on static page?
 
When page will be fully loaded you should create nextrtc object.
If you don’t know when your page is fully loaded you can use override method NextRTC.onReady (this way of use is presented in example).

When you create NextRTC object you have to provide function which will be called when event happens.
To register function you have to call method on() as presented in snipped:

```js
var nextRTC = new NextRTC({
    ...
});

nextRTC.on('{eventName}', function(nextrtc:NextRTC, event:Event){
    
});
```
There are two signals which are providing other second parameter type. Those signals are:
`localStream` and `remoteStream`, when you are handling local audio/video stream and incoming audio/video stream you can simply attach stream to valid element (without additional action like resolving stream by description provided in event).

```js
nextRTC.on('{localStream|remoteStream}', function(nextrtc:NextRTC, stream:Stream){

});
```
Event structure and available events are presented [here](https://github.com/mslosarz/nextrtc-signaling-server)

Event is serialized java version of message.