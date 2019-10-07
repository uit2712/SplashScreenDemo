# SplashScreenDemo
Splash screen in React Native

<b>----------------------SPLASH SCREEN IN REACT NATIVE----------------------</b><br>
<b>1) Step 1</b>: Install necessary module 'react-native-splash-screen':
npm i react-native-splash-screen --save
<b>2) Step 2</b>: Link module 'react-native-splash-screen' to our project and do some settings to use splash screen:<br>
<b>a)</b> Go to file 'MainApplication.java'<br>
<b>b)</b> Add these lines into file 'android/settings.gradle'

<pre>
	include ':react-native-splash-screen'
	project(':react-native-splash-screen').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splash-screen/android')
  </pre>

<b>c)</b> Add this line into file 'android/app/build.gradle' in section 'dependencies'

<pre>
dependencies {
    implementation project(':react-native-splash-screen') // here
    ...
}
</pre>
<b>d)</b> In file 'MainApplication.java', using package 'SplashScreenReactPackage':
<pre>
	import org.devio.rn.splashscreen.SplashScreenReactPackage;

	.....
	@Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
            new SplashScreenReactPackage() // here
      );
    }
</pre>
<b>e)</b> Settings: in file 'MainActivity.java' import package base on your module version 'react-native-splash-screen', my version >= 0.3.1
<pre>
	// react-native-splash-screen >= 0.3.1
	import org.devio.rn.splashscreen.SplashScreen; // here
	// react-native-splash-screen < 0.3.1
	import com.cboy.rn.splashscreen.SplashScreen; // here
	</pre>
<b>f)</b> Import package Bundle (if it does not exist):
<pre>
import android.os.Bundle; // here
	</pre>
<b>g)</b> After that, add this line to function 'onCreate()' or create if it does not exist
<pre>
	@Override
    protected void onCreate(Bundle savedInstanceState) {
        SplashScreen.show(this);  // here
        super.onCreate(savedInstanceState);
    }
</pre>
<b>3) Step 3</b>: Create file called 'launch_screen.xml' in folder 'android/app/src/main/res/layout'
(create folder 'layout' if it does not exist). The contents of this file:

<b>a)</b> If you want to show static image as a splash screen, use this:
<pre>
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"&gt;
    &lt;ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/launch_screen" android:scaleType="centerCrop" /&gt;
&lt;/RelativeLayout&gt;
</pre>
<b>b)</b> Or, If you want to show dynamic image (gif) as a splash screen, use this:
<pre>
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"&gt;
    &lt;pl.droidsonroids.gif.GifTextView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@drawable/launch_screen"
    /&gt;
&lt;/RelativeLayout&gt;
</pre>
And also add this line in file 'android/app/build.gradle'
<pre>
dependencies {
	...
    compile 'pl.droidsonroids.gif:android-gif-drawable:1.2.10' // here
    ...
}
</pre>
<b>4) Step 4</b>: Add image splash screen:

In <b>'Step 3'</b>: we have this line:
<pre>
	&lt;ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/launch_screen" android:scaleType="centerCrop" /gt;
</pre>
or this line:
<pre>
	&lt;pl.droidsonroids.gif.GifTextView
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:background="@drawable/launch_screen"
	    /gt;
</pre>
And you see that we have '@drawable/launch_screen', here 'launch_screen' is the name of image
as a splash screen in the folder 'drawable', so let create a folder 'drawable' in
'android/app/src/main/res/' and add image 'launch_screen' to this folder<br>
<b>5) Step 5</b>: It is time to show our splash screen, in component that you want to show splash screen:
<b>a)</b> Import module 'react-native-splash-screen':

import SplashScreen from 'react-native-splash-screen';

<b>b)</b> I want to hide splash screen after 3 seconds:
<pre>
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
</pre>
<b>THANK YOU FOR WATCHING VIDEO, REMEMBER TO LIKE AND SUBSCRIBE FOR NEW VIDEOS</b>
