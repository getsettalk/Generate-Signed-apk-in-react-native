# Generate-Signed-apk-in-react-native
How to make signed release apk in react-native


- ![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) ***First of all, make sure your Android project is error free. That means, it is compiling and running successfully on the emulator or on an Android device Thus, open the Android project using Android Studio or run it from the command line. If everything compiles as expected you are good to go***

# - ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 1. Generate a keystore :
 To generate keystore use this command: (at root Level)
 ```
 keytool -genkey -v -keystore your_key_name.keystore -alias your_key_alias -keyalg RSA -keysize 2048 -validity 10000
 ```
You can change **your_key_name** with any name you want, as well as **your_key_alias**. This key uses key-size 2048, instead of default 1024 for security reason.

Thus, this command prompts you for the password of the keystore, the actual key, and the distinguished name fields for your key. Hence, everything should be entered manually and carefully:

> Enter your keystore password: password123

> Re-enter new password: password123

> What is your first and last name? [unknown]: Sujeet Kumar

> What is the name of your organizational unit? [unknown]: Sample Company

> What is the name of your organization? [unknown]: Sample

> What is the name of your city or Locality? [unknown]: XYZ

> What is the name of your State or Province? [unknown]: ABC

> What is the two-letter country code for this unit? [unknown]: 91

# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 2. Adding Keystore to your project
  Firstly, you need to copy the file **your_key_name.keystore** and paste it under the android/app directory in your React Native project folder.

![image](https://user-images.githubusercontent.com/49394996/212828707-f0261c96-7b0e-46dc-8730-86ccb7d1e0c4.png)



# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 3.Do changes in Some file:
~check below for seprate~
You need to open your `android\app\build.gradle` file and add the keystore configuration. There are two ways of configuring the project with keystore. First, the common and unsecured way:

```
android {
....
  signingConfigs {
   release {
      storeFile file('your_key_name.keystore')
      storePassword 'your_key_store_password'
      keyAlias 'your_key_alias'
      keyPassword 'your_key_file_alias_password'
    }
  }
  buildTypes {
    release {
      ....
      signingConfig signingConfigs.release
    }
  }
}
```

**You Have Just Add this Line at signingConfigs Block**

```diff
 release {
      storeFile file('your_key_name.keystore')
      storePassword 'your_key_store_password'
      keyAlias 'your_key_alias'
      keyPassword 'your_key_file_alias_password'
    }
```
**And Add this to  buildTypes {
    release {  Block**
    
```
buildTypes {
    release {
      ....
      signingConfig signingConfigs.release  <----- Only This Comment Debug Line
    }
  }
  ```

# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 4.Run This Command :

to create Media files.make sure you have an `assets` folder under `android/app/src/main/assets`. If it’s not there, create one. Then run the following command to build the bundle.

### Create folder inside :
 > assets  ``android/app/src/main/assets``

```
npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```

# 5. Delete these folder (automatic created newly ) :
![image](https://github.com/getsettalk/Generate-Signed-apk-in-react-native/assets/49394996/0e1638c0-ecae-48ed-a763-92677f99009d)


> E:\React-Native\MlmNetworking\android\app\src\main\res\drawable-hdpi

> E:\React-Native\MlmNetworking\android\app\src\main\res\drawable-mdpi

> E:\React-Native\MlmNetworking\android\app\src\main\res\drawable-xhdpi

> E:\React-Native\MlmNetworking\android\app\src\main\res\drawable-xxhdpi

> E:\React-Native\MlmNetworking\android\app\src\main\res\drawable-xxxhdpi  

As Showing in above image you have to delete that it may conflict when building

# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 6. Release APK Generation:
Place your terminal directory to android using:
```
cd android
```
>> For Windows,
```
gradlew assembleRelease 
```
>> For Linix and Mac

``` 
./gradlew assembleRelease
```

>> For generate  .aab 
```
cd android
./gradlew bundleRelease
```


## Log your apk to mac and window

### MacOS detect apk log:
Option MacOs 1: Disable extended globbing for the command: You can disable extended globbing by running the following command before using the adb logcat command:

```
set +o extendedglob
```

Option 2: Use single quotes to prevent globbing: Enclose the arguments in single quotes to prevent zsh from interpreting the * character:

```
adb logcat '*:S' 'ReactNative:V' 'ReactNativeJS:V'
```


### For windows detect log:
```
adb logcat *:S ReactNative:V ReactNativeJS:V
```

## Install Apk directly 
```
adb install android/app/build/outputs/apk/release/app-release.apk

```



# Generate SignIn Report
using this command (debug):
```
keytool -keystore android/app/debug.keystore -list -v
```

you can either navigate to this directory `android/app/`

for release, you have to write that keystore file name with extension and this will ask passoword after execution

To generate a certificate run
```
cd android && ./gradlew signingReport
```
