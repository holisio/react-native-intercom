# react-native-intercom
React Native wrapper for Intercom.io. Based off of [intercom-cordova](https://github.com/intercom/intercom-cordova)

Install
=======

IOS
---

1. `npm install react-native-intercom`
2. In XCode, in the project navigator right click `Libraries` ➜ `Add Files to [your project's name]`
3. Go to `node_modules` ➜ `react-native-intercom`➜ iOS and add `IntercomWrapper.h` and `IntercomWrapper.m`
4. Add `pod 'Intercom'` to your Podfile and run `pod install`. More instructions here: [Intercom for iOS](https://github.com/intercom/intercom-ios)
5. Initialize Intercom in your `AppDelegate.m`
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Initialize Intercom
    [Intercom setApiKey:@"<#ios_sdk-...#>" forAppId:@"<#your-app-id#>"];
}
```

Android
-------
1. in `android/settings.gradle`
   ```
   ...
include ':react-native-intercom'
project(':react-native-intercom').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-intercom/android')
   ```

2. in `android/app/build.gradle` add:
   ```
   dependencies {
       ...
	   compile project(':react-native-intercom')
   }
   ```

3. and finally, in `android/src/main/java/com/{YOUR_APP_NAME}/MainActivity.java` add:
   ```java
   //...
   com.robinpowered.react.Intercom.IntercomPackage; // <--- This!
   //...
   @Override
   protected List<ReactPackage> getPackages() {
     return Arrays.<ReactPackage>asList(
       new MainReactPackage(),
       new IntercomPackage() // <---- and This!
     );
}
   ```
4. IMPORTANT! In order to allow Android to work with Intercom, please follow the instructions here: [Intercom for Android](https://github.com/intercom/intercom-android)


Usage
=====
### Require the module
```javascript
var Intercom = require('react-native-intercom');
```

### Log an event
```javascript
Intercom.logEvent('viewed_screen', { extra: 'metadata' });
```

### Register a Logged In user
```javascript
Intercom.registerIdentifiedUser({ userId: 'bob' });
```

### Register a Logged In user and post extra metadata
```javascript
Intercom.registerIdentifiedUser({ userId: 'bob' })
.then(() => {
	console.log('registerIdentifiedUser done');

	return Intercom.updateUser({
		email: 'email',
		name: 'name',
	});
})
.catch((err) => {
	console.log('registerIdentifiedUser ERROR', err);
});
```

### Sign Out
```javascript
Intercom.reset()
```

### Show Message Composer
```javascript
Intercom.displayMessageComposer();
```
