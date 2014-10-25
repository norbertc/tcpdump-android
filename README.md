Overview
--------
This script will cross compile tcpdump for use on Android devices.

It was written by Loic Poulain on OMAPpedia. See http://omappedia.org/wiki/USB_Sniffing_with_tcpdump for full details.
Modified by Norbert Copones.

Build
-----
Patch tcpdump configure script using the diff below:

   --- configure.old
   +++ configure
   @@ -5107,7 +5107,7 @@
      $as_echo_n "(cached) " >&6
    else
      if test "$cross_compiling" = yes; then :
   -  td_cv_buggygetaddrinfo=yes
   +  td_cv_buggygetaddrinfo=no
    else
      cat confdefs.h - <<_ACEOF >conftest.$ac_ext
    /* end confdefs.h.  */

Install the [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) then:  

    export NDK=/path/to/ndk 
    ./build-tcpdump

Install on Android
------------------
    > adb push tcpdumpbuild/tcpdump /sdcard
    > adb shell
    # su
    # mount -o remount,rw /system
    # cp /sdcard/tcpdump /system/xbin/tcpdump
    # chmod 755 /system/xbin/tcpdump
    # chown 0:0 /system/xbin/tcpdump
    # mount -o remount,ro /system
