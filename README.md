Overview
--------
This script will cross compile tcpdump for use on Android devices.

It was written by Loic Poulain on OMAPpedia. See http://omappedia.org/wiki/USB_Sniffing_with_tcpdump for full details.
Modified by Norbert Copones for Android Marshmallow and arm64.

Build
-----
Install the [Android NDK](https://developer.android.com/ndk/downloads/index.html) then:  

    NDK=/path/to/ndk ./build-tcpdump

By default, aarch64 binaries will be built. To build for arm 32-bit:

   NDK=/path/to/ndk ARCH=arm ./build-tcpdump

Install on Android
------------------
    $ adb push tcpdumpbuild/tcpdump /sdcard/
    $ adb shell
    # su
    # mount -o remount,rw /system
    # cp /sdcard/tcpdump /system/xbin/tcpdump
    # chmod 755 /system/xbin/tcpdump
    # chown 0:0 /system/xbin/tcpdump
    # mount -o remount,ro /system
