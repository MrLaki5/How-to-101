## Instructions for unzipping and after that zipping and signing android app:


* Apktool can be downloaded from [here](https://ibotpeaches.github.io/Apktool/install/)


* Decode (unzip) android apk file:
``` bash
apktool d <application_name>.apk
```


* After previous step contents of apk can be viewed and changed.


* Encode (zip) android unzipped application into apk file:
``` bash
apktool b <path_to_unzipped_android_app_folder>
# After this step, apk is situatied in <path_to_unzipped_android_app_folder>/dist/<application_name>.apk
```


* Sign newely created apk file:
``` bash
jarsigner -verbose -keystore ~/.android/debug.keystore -storepass android -keypass android <path_to_unzipped_android_app_folder>/dist/<application_name>.apk androiddebugkey
# Note: jarsigner is part of jdk
# -keystore: In command from above default android studio debug keystore is used
```

