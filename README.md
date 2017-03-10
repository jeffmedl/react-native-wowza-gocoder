
# react-native-wowza-gocoder

## Getting started

`$ npm install react-native-wowza-gocoder --save`

### Mostly automatic installation

`$ react-native link react-native-wowza-gocoder`

### Manual installation


#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-wowza-broadcaster` and add `RNWowzaBroadcaster.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNWowzaBroadcaster.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

##### Post installation iOS
1. After obtainting WowzaGoCoderSDK framework and the wowzastaticlib, add them to your main project, in the root directory of the project
2. Add the libraries to the build phases for your app target, add a copy files phase http://www.wowza.com/resources/gocodersdk/docs/1.0/intro-installation/

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.rngocoder.RNWowzaBroadcasterPackage;` to the imports at the top of the file
  - Add `new RNWowzaBroadcasterPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-wowza-broadcaster'
  	project(':react-native-wowza-broadcaster').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-wowza-broadcaster/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-wowza-broadcaster')
  	```
##### Post installation Android
1. After obtainting WowzaGoCoderSDK aar file, add them to your nodemodules/react-native-wowza-gocoder to the libs directory
2. http://www.wowza.com/resources/gocodersdk/docs/1.0/intro-installation/

## Usage
```javascript
import BroadcastView from 'react-native-wowza-broadcaster';

  <BroadcastView style= {yourStyle}
                 hostAddress = {hostaddress}
                 applicationName = {applicationName}
                 streamName = {streamName}
                 broadcasting = {false} //change this value to start broadcast
                 username = {username}
                 password = {password}
                 sizePreset = {3}
                 port={}//default is 1935
                 muted = {false}
                 flashOn = {false}
                 frontCamera =  {false}
                 onBroadcastStart= {}
                 onBroadcastFail= {}
                 onBroadcastStatusChange= {}
                 onBroadcastEventReceive= {}
                 onBroadcastErrorReceive= {}
                 onBroadcastVideoEncoded = {}
                 onBroadcastStop = {}
                 >
  </BroadcastView>
  ;
  
  //Using the broadcast module
  var BroadcastManager =  NativeModules.BroadcastModule;
  
  BroadcastManager.startTimer(1, 3600);// first argument - timer interval, second argument time to timeout timer in seconds
  
  //Add listener to update broadcast time, callback will be fired by interval set when the timer was started
  DeviceEventEmitter.addListener('broadcastTimer', (seconds) => {
          //amount of time passed in seconds 
  });
        
  BroadcastManager.stopTimer();
```
  