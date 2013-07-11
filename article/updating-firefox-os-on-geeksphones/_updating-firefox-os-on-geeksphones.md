# Updating Firefox OS On Geeksphones

#### 31st of May, 2013

If you are one of the lucky guys owning a geeksphone you may have thought about updating to a nightly build. Since geeksphone publishes stable releases over the air you should already have the latest stable version installed. Updating to a nightly build is pretty easy if you don’t want a custom build. This small guide is for Mac OS X. Updating on Linux or Windows is slightly different.

## Installing adb and fastboot

`adb` and `fastboot` are small executables provided by the Android SDK. Simply download the Android SDK from [the official website](http://developer.android.com/sdk/index.html) and unzip the file. Then open the folder __platform-tools__ inside of __sdk__ and copy the files __adb__ and __fastboot__ to a folder in your PATH, e.g. `/bin/`.

## Download the latest nightly build

Now head over to [geeksphone’s official images](http://downloads.geeksphone.com/) and download the latest nightly build for your device, which you’ll also have to unzip.

## Updating your device

Before the final step be sure that your device has at least 50% power. If that’s the case connect it to your Mac via USB and open the unzipped folder with the image from geeksphone in terminal. Now simply flash the phone by executing:

	./flash_mac.sh

The command should now flash your phone and run the update. Just wait until the device automatically restarts and don’t try turning it on if the screen goes black.

Have fun with the latest builds!

<h3 class="space-above">Further Reading</h3>

- [geeksphones official guide](http://downloads.geeksphone.com/drivers/Manual_flash_geeksphone-eng.txt)
- [geeksphones forum](http://forum.geeksphone.com/)
- [geeksphones manifests](http://www.geeksphone.com/manifests/index.php)
