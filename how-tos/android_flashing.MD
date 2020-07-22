## Flashing android images

* To be able to flash images SDK Platform Tools are needed. Download link: https://developer.android.com/studio/releases/platform-tools.html
* Beside that on OSX Android File Transfer is needed for system to see device. Download link: https://www.android.com/filetransfer/
* Also image of system that we want to flash is needed. Official images can be downloaded here: https://developers.google.com/android/images
* Unzip SDK Platform Tools and android image to same directory.
* Open terminal and go to unziped directory.
* On phone developer options must be activated. USB debugging and OEM unlocking turned ON.
* Turn off phone.
* Turn on phone with holding power and volume down buttons. Phone should open fastboot screen.
* Connect phone to computer.
* Unlock fastboot mode with command from terminal:
``` bash
 ./fastboot flashing unlock
```
* Now when phone is unlocked we can put image on it. But first we have to fix ./flash-all.sh script.
* Open ./flash-all.sh script in editor:
``` bash
nano ./flash-all.sh
```
* In editor remove if structure and add ./ before every fastboot command. Example:
From:
``` bash
	#!/bin/sh

	# Copyright 2012 The Android Open Source Project
	#
	# Licensed under the Apache License, Version 2.0 (the "License");
	# you may not use this file except in compliance with the License.
	# You may obtain a copy of the License at
	#
	#      http://www.apache.org/licenses/LICENSE-2.0
	#
	# Unless required by applicable law or agreed to in writing, software
	# distributed under the License is distributed on an "AS IS" BASIS,
	# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	# See the License for the specific language governing permissions and
	# limitations under the License.

	if ! grep -q partition-exists $(which fastboot); then
	  echo "fastboot too old; please download the latest version at https://developer.android.com/studio/releases/platform-tools.html"
	  exit 1
	fi
	fastboot flash bootloader bootloader-bonito-b4s4-0.1-5653622.img
	fastboot reboot-bootloader
	sleep 5
	fastboot flash radio radio-bonito-g670-00011-190411-b-5457439.img
	fastboot reboot-bootloader
	sleep 5
	fastboot -w update image-bonito-pq3b.190801.002.zip
```

To:

``` bash
	#!/bin/sh

	# Copyright 2012 The Android Open Source Project
	#
	# Licensed under the Apache License, Version 2.0 (the "License");
	# you may not use this file except in compliance with the License.
	# You may obtain a copy of the License at
	#
	#      http://www.apache.org/licenses/LICENSE-2.0
	#
	# Unless required by applicable law or agreed to in writing, software
	# distributed under the License is distributed on an "AS IS" BASIS,
	# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	# See the License for the specific language governing permissions and
	# limitations under the License.
	./fastboot flash bootloader bootloader-bonito-b4s4-0.1-5653622.img
	./fastboot reboot-bootloader
	sleep 5
	./fastboot flash radio radio-bonito-g670-00011-190411-b-5457439.img
	./fastboot reboot-bootloader
	sleep 5
	./fastboot -w update image-bonito-pq3b.190801.002.zip
```
* After editing is done if nano editor was used press ctrl + X and then type Y and press enter to save changes.
* Now run script with:
``` bash
./flash-all.sh
```
* After script is done android system should start on phone.
* Now last step is to turn off fastboot mode.
* Turn off phone.
* Turn phone on with holding power and volume down button. Phone should open in fastboot mode.
* Now in terminal run command: 
``` bash
./fastboot flashing lock
```
* This should lock the fastboot mode. 
* Now system can be set up and used normaly.
