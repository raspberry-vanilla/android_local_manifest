### Device specific configuration to build AOSP Android 13 for Raspberry Pi 4.

***

### How to build:

1. Establish [Android build environment](https://source.android.com/setup/initializing) and install [repo](https://source.android.com/docs/setup/develop#installing-repo).

2. Install additional packages:

```
sudo apt-get install bc coreutils dosfstools e2fsprogs fdisk kpartx mtools ninja-build pkg-config python3-pip
sudo pip3 install meson mako jinja2 ply pyyaml dataclasses
```

3. Initialize repo:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r75
curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-13.0/manifest_brcm_rpi4.xml
```

Or optionally, you can reduce download size by creating a shallow clone and removing unneeded projects:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r75 --depth=1
curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-13.0/manifest_brcm_rpi4.xml
curl --create-dirs -L -o .repo/local_manifests/remove_projects.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-13.0/remove_projects.xml
```

4. Sync source code:

```
repo sync
```

5. Setup Android build environment:

```
. build/envsetup.sh
```

6. Select build target:

Tablet UI:
```
lunch aosp_rpi4-userdebug
```

Android TV:
```
lunch aosp_rpi4_tv-userdebug
```

Android Automotive:
```
lunch aosp_rpi4_car-userdebug
```

7. Compile:
```
make bootimage systemimage vendorimage -j$(nproc)
```

8. Make flashable image:

```
./rpi4-mkimg.sh
```

Also look into [Linux kernel build instructions](https://github.com/raspberry-vanilla/android_kernel_manifest/tree/android-13.0).

***

### Issues:

- [Android](https://github.com/raspberry-vanilla/android_local_manifest/issues)
- [Linux kernel](https://github.com/raspberry-vanilla/android_kernel_manifest/issues)

***

### Wiki:

- [Audio](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Audio)
- [DSI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/DSI-display)
- [HDMI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/HDMI-display)
- [HDMI-CEC](https://github.com/raspberry-vanilla/android_local_manifest/wiki/HDMI-CEC)
- [Interfaces](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Interfaces)
- [USB boot](https://github.com/raspberry-vanilla/android_local_manifest/wiki/USB-boot)
- [Video decoding & encoding](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Video-decoding-&-encoding)
