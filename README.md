
# react-native-wowza-gocoder

## About
This is a Native Module for React Native that allows integration of Wowza's GoCoder SDK in less time.  It has been battle tested on our internal and client projects.  !Note* we require RN 0.42+ for this to work!  

## Getting started

`$ npm install react-native-wowza-gocoder --save`

### Mostly automatic installation

`$ react-native link react-native-wowza-gocoder`

### Manual installation


#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-wowza-gocoder` and add `RNWowzaBroadcaster.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNWowzaBroadcaster.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

##### Post installation iOS
1. After obtaining WowzaGoCoderSDK framework and the wowzastatic-lib, add them both to a folder in the root directory of the project.
2. Add the WowzaGoCoderSDK.framework to the build phases for your app target, add a copy files phase with the WowzaGoCoder.SDK http://www.wowza.com/resources/gocodersdk/docs/1.0/intro-installation/

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.rngocoder.RNWowzaBroadcasterPackage;` to the imports at the top of the file
  - Add `new RNWowzaBroadcasterPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-wowza-gocoder'
  	project(':react-native-wowza-gocoder').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-wowza-gocoder/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-wowza-gocoder')
  	```

##### Post installation Android
1. After obtaining WowzaGoCoderSDK aar file, add it to your nodemodules/react-native-wowza-gocoder to the libs directory(create it if needed)
2. http://www.wowza.com/resources/gocodersdk/docs/1.0/intro-installation/

## Usage

1. Import the module
`import BroadcastView from 'react-native-wowza-gocoder';`
2. Set a config
  ```javascript
  const config ={
    hostAddress:'',
    applicationName:'',
    username:'',
    password:'',
    streamName:'',
    sdkLicenseKey:''
  };
  ```
  
3. Add functions for debug, testing
  ```javascript 
  onBroadcastStart(){
    console.log("Bcast start");
  }
  onBroadcastFail(){
    console.log("Bcast fail");
  }
  onBroadcastStatusChange(){
    console.log("Bcast status change");
  }
  onBroadcastEventReceive(){
    console.log("Bcast event receive");
  }
  onBroadcastErrorReceive(){
    console.log("Bcast error receive");
  }
  onBroadcastVideoEncoded(){
    console.log("Bcast encoded");
  }
  onBroadcastStop(){
    console.log("Bcast stop");
  }
  ```
  
4. Use the component in render
```javascript 
<BroadcastView style= {styles.videoContainer}
                     hostAddress = {config.hostAddress}
                     applicationName = {config.applicationName}
                     broadcastName={config.streamName}
                     broadcasting = {false}
                     username = {config.username}
                     password = {config.password}
                     sizePreset = {3}
                     port={1935}
                     muted = {false}
                     flashOn = {false}
                     frontCamera =  {false}
                     onBroadcastStart= {this.onBroadcastStart}
                     onBroadcastFail= {this.onBroadcastFail}
                     onBroadcastStatusChange= {this.onBroadcastStatusChange}
                     onBroadcastEventReceive= {this.onBroadcastEventReceive}
                     onBroadcastErrorReceive= {this.onBroadcastErrorReceive}
                     onBroadcastVideoEncoded = {this.onBroadcastVideoEncoded}
                     onBroadcastStop = {this.onBroadcastStop}
                     sdkLicenseKey={config.sdkLicenseKey}
      >
  </BroadcastView> 
  ```
 
 
5. Be sure to use absolute positioning on your styles otherwise the video may not show correctly
  ```javascript 

  const styles = StyleSheet.create({
    container: {
      flex: 1,
    },
    videoContainer:{
      position:'absolute',
      top:0,
      left:0,
      right:0,
      bottom:40
    }
  });
  ```
* Optional: If you are familiar with controlling state then you could trigger start/stop of streaming by passing state in the BroadcastView component prop broadcasting.  example broadcasting = {false} to broadcasting = {this.state.brodcasting} *
  //Using the broadcast module
  
    `var BroadcastManager =  NativeModules.BroadcastModule;`
  
    `BroadcastManager.startTimer(1, 3600);`
* Android only - first argument - timer interval, second argument time to timeout timer in seconds
  
* Stop Timer when stopping the broadcast - Android only       
    `BroadcastManager.stopTimer();`

## Running the example project

### iOS
1. Install and link dependencies
```
cd react-native-wowza-gocoder/example
npm install
react-native-link
```
2. Download the GoCoder SDK - https://www.wowza.com/pricing/installer#gocodersdk-downloads
3. Unzip and add "wowzagocoder_static_lib" and "WowzaGoCoderSDK.framework" to /example/ios/
4. Open /example/ios/example.xcodeproj in Xcode
5. From the Xcode Project Navigator, select the "example" project and the "example" target
6. On the "General" tab configure the "Identity" settings with your app bundle identifier (should match the bundleID tied to your GoCoder license)
    * If you don't have a license key you can register for a free trial: https://www.wowza.com/products/gocoder/sdk/trial
7. Configure your "Signing" settings with your provisioning profiles
8. Configure your GoCoder license key and Wowza server settings in example/index.js as shown in the [Usage](#usage) section above
9. Run your project on a device (will not work on simulator)

### Android
Coming soon

## TODOS

- [ ] Add better support for the size preset props for both platforms
- [ ] Add a config for the different keys provided per platform
- [ ] Create a sample project for Android
