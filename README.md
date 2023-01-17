# Generate-Signed-apk-in-react-native
How to make signed release apk in react-native


- ![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) ***First of all, make sure your Android project is error free. That means, it is compiling and running successfully on the emulator or on an Android device Thus, open the Android project using Android Studio or run it from the command line. If everything compiles as expected you are good to go***

# - ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 1. Generate a keystore :
 To generate keystore use this command:
 ```
 keytool -genkey -v -keystore your_key_name.keystore -alias your_key_alias -keyalg RSA -keysize 2048 -validity 10000
 ```
