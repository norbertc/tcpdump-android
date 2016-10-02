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

In case, libpcap configure script is having an issue detecting getifaddrs(), patch libpcap configure script:

    patch -p0 < libpcap-configure

Build using ./build-tcpdump

Build with BoringSSL (optional)
-------------------------------

To build with BoringSSL libcrypto support, [compile BoringSSL](https://boringssl.googlesource.com/boringssl/+/HEAD/BUILDING.md).
Copy BoringSSL include/openssl and headers to the NDK platform include directory (e.g. NDK_ROOT/platforms/android-23/arch-arm64/usr/include):

    e.g.
    cd /path/to/BoringSSL/source
    cd include
    cp -r openssl /NDK_ROOT/platforms/android-XX/<arch>/usr/include

Copy BoringSSL libcrypto.so and libssl.so to the NDK platform lib directory (e.g. NDK_ROOT/platforms/android-23/arch-arm64/usr/lib):

    e.g.
    cd /path/to/BoringSSL/build/dir
    cp crypto/libcrypto.so NDK_ROOT/platforms/android-XX/<arch>/usr/lib
    cp ssl/libssl.so NDK_ROOT/platforms/android-XX/<arch>/usr/lib

Patch the configure and configure.in file:

    patch -p0 < configure.patch
    patch -p0 < configure.in.patch

Build using ./build-tcpdump

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
