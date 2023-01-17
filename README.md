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

Enter your keystore password: password123

Re-enter new password: password123

What is your first and last name? [unknown]: Sujeet Kumar

What is the name of your organizational unit? [unknown]: Sample Company

What is the name of your organization? [unknown]: Sample

What is the name of your city or Locality? [unknown]: XYZ

What is the name of your State or Province? [unknown]: ABC

What is the two-letter country code for this unit? [unknown]: 91

# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 2. Adding Keystore to your project
  Firstly, you need to copy the file **your_key_name.keystore** and paste it under the android/app directory in your React Native project folder.

![image](https://user-images.githubusercontent.com/49394996/212828707-f0261c96-7b0e-46dc-8730-86ccb7d1e0c4.png)



# ![#FF0032](https://placehold.co/15x15/FF0032/FF0032.png)Step 3.Do changes in Some file:

You need to open your android\app\build.gradle file and add the keystore configuration. There are two ways of configuring the project with keystore. First, the common and unsecured way:

