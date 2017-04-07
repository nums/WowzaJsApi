<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [WowzaAPI](#wowzaapi)
    -   [getStreamFilesList](#getstreamfileslist)
    -   [getStreamConfiguration](#getstreamconfiguration)
    -   [createRecorder](#createrecorder)
    -   [stopRecording](#stoprecording)
    -   [getRecordersList](#getrecorderslist)
    -   [connectStreamFile](#connectstreamfile)
    -   [disconnectStreamFile](#disconnectstreamfile)

## WowzaAPI

**Extends Object**

This class is JavaScript wrapper for cURL REST API for Wowza Streaming Engine server <br>
_tested with NodeJS version 6.10.2 LTS_

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** possible to set stream parametres which will use as default for methods
    -   `options.wowzaAdress` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** IP address or domein name of Wowza Streaming Engine (optional, default `'localhost'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (optional, default `'myStream.stream'`)
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (optional, default `'application'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application instance (optional, default `'_definst_'`)
    -   `options.mediaCasterType` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** caster type (optional, default `'rtp'`)

**Examples**

```javascript
let Wowza = require('./wowza.js');
wowza = new Wowza({
	wowzaAdress: '192.168.1.15',   // default value is 'localhost'
	streamFile: 'ipCamera.stream', // default is 'myStream.stream'
	application: 'webrtc',         // default is 'live'
	appIstance: '_definst_',       // default is '_definst_'
	mediaCasterType: 'rtp'         // default is 'rtp'
});
wowza.someWowzaMethod(); // now you can use the JS wowza API.
```

### getStreamFilesList

Get a list of streamfiles

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)

**Examples**

```javascript
wowza.getStreamFilesList({application: 'webrtc', streamFile: 'ipCamera'})
	.then( responseMsg => console.log(responseMsg))
	.catch( errorMsg => console.log(errorMsg));

// Wowza answer example:
//{serverName: '_defaultServer_', streamFiles: [{id: 'ipCamera2', href: '/v2/servers/_defaultServer_/vhosts/_defaultVHost_/applications/webrtc/streamfiles/ipCamera2'}]}
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve by object which contains array of streamFiles and it's confifurations

### getStreamConfiguration

Get specific stream configuration

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (default value can be another if it was passed to the class constructor) (optional, default `'myStream.stream'`)

**Examples**

```javascript
wowza.getStreamConfiguration()
.then(response => console.log(response))
.catch(errorMsg => console.log(errorMsg));
// Wowza answer example: 
// {version: '1488715914000', serverName: '_defaultServer_', uri: 'rtsp://admin:admin@192.168.42.231', name: 'ipCamera'}
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve by stream configurations object

### createRecorder

Create Recorder

**Parameters**

-   `recorderParametres` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `recorderParametres.restURI` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.recorderName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.instanceName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.recorderState` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.defaultRecorder` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
    -   `recorderParametres.segmentationType` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.outputPath` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** default value is \[] and wowza should save files in [install-dir]/content, not tested
    -   `recorderParametres.baseFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** default is \[], and wowza should name file as a streamfile name, not tested
    -   `recorderParametres.fileFormat` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.fileVersionDelegateName` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.fileTemplate` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.segmentDuration` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
    -   `recorderParametres.segmentSize` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
    -   `recorderParametres.segmentSchedule` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
    -   `recorderParametres.recordData` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
    -   `recorderParametres.startOnKeyFrame` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
    -   `recorderParametres.splitOnTcDiscontinuity` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
    -   `recorderParametres.backBufferTime` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
    -   `recorderParametres.option` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** should to work with one of: version | append | overwrite, but not tested
    -   `recorderParametres.moveFirstVideoFrameToZero` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
    -   `recorderParametres.currentSize` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
    -   `recorderParametres.currentDuration` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** 
    -   `recorderParametres.recordingStartTime` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (default value can be another if it was passed to the class constructor) (optional, default `'myStream.stream'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an instance (default value can be another if it was passed to the class constructor) (optional, default `'_definst_'`)

**Examples**

```javascript
wowza.createRecorder({
	"restURI": "http://192.168.1.15:8087/v2/servers/_defaultServer_/vhosts/_defaultVHost_/applications/webrtc/instances/_definst_/streamrecorders/ipCamera.stream",
	"recorderName": "ipCameraRecorder",
	"instanceName": "_definst_",
	"recorderState": "Waiting for stream",
	"defaultRecorder": true,
	"segmentationType": "None",
	"outputPath": "", // default value is [] and wowza save files in [install-dir]/content, not tested
	"baseFile": "myrecord2.mp4", // default is [], and wowza will name file as a streamfile name, not tested
	"fileFormat": "MP4",
	"fileVersionDelegateName": "com.wowza.wms.livestreamrecord.manager.StreamRecorderFileVersionDelegate",
	"fileTemplate": "${BaseFileName}_${RecordingStartTime}_${SegmentNumber}",
	"segmentDuration": 900000,
	"segmentSize": 10485760,
	"segmentSchedule": "0 * * * * *",
	"recordData": true,
	"startOnKeyFrame": true,
	"splitOnTcDiscontinuity": false,
	"backBufferTime": 3000,
	"option": "Version existing file", //should to work with one of: version | append | overwrite, but not tested
	"moveFirstVideoFrameToZero": true,
	"currentSize": 0,
	"currentDuration": 0,
	"recordingStartTime": ""
},{
	streamFile: 'ipCamera', 
	application: 'webrtc',
	appIstance: '_definst_'
})
	.then(response => console.log(response))
	.catch(errorMsg => console.log(errorMsg));
// Wowza answer example: 
//{ success: true, message: 'Recorder Created', data: null }
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve when rec will start

### stopRecording

Stop recording

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (default value can be another if it was passed to the class constructor) (optional, default `'myStream.stream'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an instance (default value can be another if it was passed to the class constructor) (optional, default `'_definst_'`)

**Examples**

```javascript
wowza.stopRecording({
	streamFile: 'ipCamera', 
	application: 'webrtc',
	appIstance: '_definst_'
}).then(response => console.log(response)).catch(errorMsg => console.log(errorMsg));
// Wowza answer example: 
// { success: true, message: 'Recording (ipCamera) stopped', data: null }
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve when rec will stop

### getRecordersList

Get a list of recorders

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an instance (default value can be another if it was passed to the class constructor) (optional, default `'_definst_'`)

**Examples**

```javascript
wowza.getRecordersList({
	application: 'webrtc',
	appIstance: '_definst_'
}).then( response => console.log(response)).catch( errorMsg => console.log(errorMsg));
// Wowza answer example: 
//{ serverName: '_defaultServer_',
//  instanceName: '_definst_',
//  streamrecorder: 
//   [ { recorderName: 'ipCamera',
//       instanceName: '_definst_',
//       recorderState: 'Waiting for stream',
//       defaultRecorder: false,
//       segmentationType: 'None',
//       outputPath: '/usr/local/WowzaStreamingEngine/content/records',
//       baseFile: 'myrecord2.mp4',
//       fileFormat: 'MP4',
//       fileVersionDelegateName: 'com.wowza.wms.livestreamrecord.manager.StreamRecorderFileVersionDelegate',
//       fileTemplate: '${BaseFileName}_${RecordingStartTime}_${SegmentNumber}',
//       segmentDuration: 900000,
//       segmentSize: 10485760,
//       segmentSchedule: '0 * * * * *',
//       recordData: true,
//       startOnKeyFrame: true,
//       splitOnTcDiscontinuity: false,
//       backBufferTime: 3000,
//       option: 'Version existing file',
//       moveFirstVideoFrameToZero: true,
//       currentSize: 0,
//       currentDuration: 0,
//       recordingStartTime: '' } ] }
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve by object contains recorders params array

### connectStreamFile

Connect a existing streamfile

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (default value can be another if it was passed to the class constructor) (optional, default `'myStream.stream'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an instance (default value can be another if it was passed to the class constructor) (optional, default `'_definst_'`)
    -   `options.mediaCasterType` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** caster type (default value can be another if it was passed to the class constructor) (optional, default `'rtp'`)

**Examples**

```javascript
wowza.connectStreamFile({
	streamFile: 'ipCamera',
	application: 'webrtc',
	appIstance: '_definst_'
}).then( response => console.log(response)).catch( errorMsg => console.log(errorMsg));
//Wowza answer example:
//{ success: true, message: 'Publish stream successfully started [webrtc/_definst_]: mp4:ipCamera.stream', data: null }
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve when stream will connect

### disconnectStreamFile

Disconnect a existing stream file

**Parameters**

-   `options` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** 
    -   `options.application` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an application (default value can be another if it was passed to the class constructor) (optional, default `'live'`)
    -   `options.streamFile` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of a streamfile (default value can be another if it was passed to the class constructor) (optional, default `'myStream.stream'`)
    -   `options.appInstance` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** name of an instance (default value can be another if it was passed to the class constructor) (optional, default `'_definst_'`)
    -   `options.mediaCasterType` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** caster type (default value can be another if it was passed to the class constructor) (optional, default `'rtp'`)

**Examples**

```javascript
wowza.disconnectStreamFile({
	streamFile: 'ipCamera.stream',
	application: 'webrtc',
	appIstance: '_definst_'
}).then( response => console.log(response)).catch( errorMsg => console.log(errorMsg));
//Wowza answer example:
//{ success: true, message: ''Publish stream successfully stopped [webrtc/_definst_]: mp4:ipCamera.stream'',data: null }
```

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise which resolve when stream will connect
