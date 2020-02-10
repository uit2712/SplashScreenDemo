# SplashScreenDemo
Splash screen in React Native

<h2>YOUTUBE VIDEO:</h2>

<h2>DEMO</h2>
<h3>Static image splash screen</h3>
<img src="https://github.com/uit2712/SplashScreenDemo/blob/master/demo/image-splash-screen.gif" title="Static image splash screen" width="600"/><br>
<h3>Gif image splash screen</h3>
<img src="https://github.com/uit2712/SplashScreenDemo/blob/master/demo/gif-splash-screen.gif" title="Gif image splash screen" width="600"/><br>

<b>----------------------SPLASH SCREEN IN REACT NATIVE----------------------</b><br>
<h2>1) Step 1</h2>: Install necessary module 'react-native-splash-screen':
npm i react-native-splash-screen --save
<h2>2) Step 2</h2>: Link module 'react-native-splash-screen' to our project and do some settings to use splash screen:<br>
<b>a)</b> Go to file 'MainApplication.java'<br>
<b>b)</b> Add these lines into file 'android/settings.gradle'

```javascript
include ':react-native-splash-screen'
project(':react-native-splash-screen').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splash-screen/android')
```

<b>c)</b> Add this line into file 'android/app/build.gradle' in section 'dependencies'

```javascript
dependencies {
    implementation project(':react-native-splash-screen') // here
    ...
}
```
<b>d)</b> In file 'MainApplication.java', using package 'SplashScreenReactPackage':
```javascript
import org.devio.rn.splashscreen.SplashScreenReactPackage;

	.....
@Override
protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
        new MainReactPackage(),
        new SplashScreenReactPackage() // here
    );
}
```
<b>e)</b> Settings: in file 'MainActivity.java' import package base on your module version 'react-native-splash-screen', my version >= 0.3.1
```javascript
// react-native-splash-screen >= 0.3.1
import org.devio.rn.splashscreen.SplashScreen; // here
// react-native-splash-screen < 0.3.1
import com.cboy.rn.splashscreen.SplashScreen; // here
```
<b>f)</b> Import package Bundle (if it does not exist):
```javascript
import android.os.Bundle; // here
```
<b>g)</b> After that, add this line to function 'onCreate()' or create if it does not exist
```javascript
@Override
protected void onCreate(Bundle savedInstanceState) {
    SplashScreen.show(this);  // here
    super.onCreate(savedInstanceState);
}
```
<h2>3) Step 3</h2>: Create file called 'launch_screen.xml' in folder 'android/app/src/main/res/layout'
(create folder 'layout' if it does not exist). The contents of this file:

<b>a)</b> If you want to show static image as a splash screen, use this:
```javascript
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/launch_screen" android:scaleType="centerCrop" />
</RelativeLayout>
```
<b>b)</b> Or, If you want to show dynamic image (gif) as a splash screen, use this:
```javascript
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <pl.droidsonroids.gif.GifTextView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@drawable/launch_screen"
    />
</RelativeLayout>
```
And also add this line in file 'android/app/build.gradle'
```javascript
dependencies {
	...
    compile 'pl.droidsonroids.gif:android-gif-drawable:1.2.10' // here
    ...
}
```
<h2>4) Step 4</h2>: Add image splash screen:

In <b>'Step 3'</b>: we have this line:
```javascript
<ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/launch_screen" android:scaleType="centerCrop" />
```
or this line:
```javascript
<pl.droidsonroids.gif.GifTextView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/launch_screen"
/>
```
And you see that we have '@drawable/launch_screen', here 'launch_screen' is the name of image
as a splash screen in the folder 'drawable', so let create a folder 'drawable' in
'android/app/src/main/res/' and add image 'launch_screen' to this folder<br>
<h2>5) Step 5</h2>: It is time to show our splash screen, in component that you want to show splash screen:<br>
<b>a)</b> Import module 'react-native-splash-screen':

```javascript
import SplashScreen from 'react-native-splash-screen';
```

<b>b)</b> I want to hide splash screen after 3 seconds:
```javascript
constructor(props: Props) {
    super(props);

    this.state = {
        splashScreenTimer: null
    };
}

componentDidMount() {
    let splashScreenTimer = setInterval(this.hideSplashScreen, 3000); // hide splash screen after 3s
    this.setState({ splashScreenTimer });
    // you can also add sound here :D
}

hideSplashScreen = () => {
    SplashScreen.hide();
    clearInterval(this.state.splashScreenTimer);
}
```
<b>THANK YOU FOR WATCHING VIDEO, REMEMBER TO LIKE AND SUBSCRIBE FOR NEW VIDEOS</b>
