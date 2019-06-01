# Samsung S8 FRP Hacking

##### There is soooo many bloated how-to-hack-and-bypass-frp-for samsung s8 and almost none actually works properly, so I have created this tutorial to keep it as simple as possible and also for myself as an reminder, this wiki is unique and using different methods than other wikis/howtos that have been published afaik. As usual, no reason for waste time to create duplicated wikis ;-)

This wiki is almost, notice _almost_ a step to step guide where I may have missed few moments. This hack require some interest and knowledge about how things work, if you are an absolute beginner with adb and heimdall then spend your time on something else or go try the tutorials you will find via google. ;-)

### DON'T GET TRICKED BY ALL APK FILES PEOPLE SAYING YOU SHOULD INSTALL

### Let's do it properly instead, see below.

### Install heimdall

##### Gentoo

    echo -e "# Heimdall (Flashtool for Sasmung Devices)\napp-mobilephone/heimdall qt5" >> /etc/portage/package.use/use
    emerge --ask app-mobilephone/heimdall

##### Debian

    apt update; apt install -qq heimdall -y

##### Windows: 

Odin is recommended Latest version can be downloaded directly from ![here](https://odindownload.com/download/Odin3_v3.13.1.zip)

### Detect Device:

    heimdall detect

### Download PIT:

    heimdall download-pit --no-reboot --output mydevice.pit

### Print PIT:

    heimdall print-pit --no-reboot --file mydevice.pit

### Boot device into flash mode:

    Poweroff device
    Press vol dn+powerbutton
    
### Flash your device with the customized rom 

I am not allowed to upload this rom here due github policy so you must go find it your self, Google is a hint ;-)

Hint: For ODIN you just need the AP field, leave other fields blank. 

### How it will look with a customized developer rom: 

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-default1.png)

### Of course you will have access to adb shell via the developer rom:

![Screenshot](https://nr1.nu//archive/samsung-s8/images/aaaaa.png)

## So now, just do as below. 

### Open notification bar: 

#### Its not possible to expand notification bar with touchscreen on the latest firmware, this can be easily bypassed by:

     adb shell cmd statusbar expand-notifications 
     
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-notifications.png)
    
    Now you have the control :-)

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-settings.png)

### Now just remove everything that should NOT be set: 

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-remocve-lock.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-remocve-lock2.png)

### Do not play with IMEI unless you know exactly what you are doing !!! IT MIGHT BRICK YOUR DEVICE !!!

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-imei.png)


![Screenshot](https://nr1.nu//archive/samsung-s8/images/notifications-exapand.png)

### Move further and delete the account added on device: 

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-delete-owner-from-this-device2.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-delete-owner-from-this-device3.png)


### Check all settings with settings list secure
#### List settings

    settings list globaL 

#### Add users when device is locked:

    settings put global add_users_when_locked 1

#### No reason to use mobile data during hacking

    settings put global mobile_data 0

#### We want to install apps to SD since otherwise shit gets protected under encryption, better to avoid this during hacking time

    settings put global add_users_when_locked force_allow_on_external 1 

#### During hacking period, we want all silent  (paranoid? ;))

    settings put global charging_sounds_enabled 0

#### Turn on bluetooth: 

    settings put global bluetooth_on 1
    
#### No reasons for count boot times:
   
    settings put global boot_count 0
    
#### Pull all pre-installed applications

    adb pull /system/priv-app/ .
    adb pull /system/app/ .

##### Once booted into FACTORY BINARY here is some more tricks that might be helpful:

#### List settings

    adb shell settings secure list

    or

    adb shell content query --uri content://settings/secure

##### Tell device that setup has been completed. 

    settings put secure user_setup_complete 1 
    or
    adb shell content insert --uri content://settings/secure --bind name:s:user_setup_complete --bind value:s:1

#### Verify the value

    adb shell content query --uri content://settings/secure|grep name=user_setup_complete|awk -F'value=' '{print $2}'|cut -d, -f1

##### Turn off location

    adb shell content insert --uri content://settings/secure --bind name:s:location_previous_mode --bind value:s:0

    adb shell content insert --uri content://settings/secure --bind name:s:location_providers_allowed --bind value:s:0

##### Turn on accessibility 

    adb shell content insert --uri content://settings/secure --bind name:s:accessibility_enabled  --bind value:s:1

##### Turn on accessibility injection

    adb shell content insert --uri content://settings/secure --bind name:s:accessibility_script_injection,  --bind value:s:1

##### Allow non market apps

    adb shell content insert --uri content://settings/secure --bind name:s:install_non_market_apps  --bind value:s:1

##### Allow push notifications and also recive sms with a popup in notifications for example:

    adb shell content insert --uri content://settings/secure --bind name:s:show_note_about_notification_hiding  --bind value:s:1

##### Disable lock feature:

    adb shell content insert --uri content://settings/secure --bind name:s:lock_function_val  --bind value:s:0

    adb shell content insert --uri content://settings/secure --bind name:s:=lock_function_val  --bind value:s:0

##### Allow us to use volume buttons:

    adb shell content insert --uri content://settings/secure --bind name:s:volume_controller_service_component  --bind value:s:1

##### Disable lockscreen, no reason for keep this 1 while we hacking =D

    adb shell content insert --uri content://settings/secure --bind name:s:lockscreen.disabled  --bind value:s:0

##### Enable max brightness (Default: 72)

     adb shell content insert --uri content://settings/secure --bind name:s:brightness_pms_marker_screen  --bind value:s:255


##### When you have edited all settings, then just erase everything to default again: 

![Screenshot](https://nr1.nu/samsung-s8/images/customized-rom-erase-device.png)

# Some more random previews from developer rom:

![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-hw.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-fail.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-water-proof.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-disableswipe.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-sysdump.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-nad.png)
![Screenshot](https://nr1.nu//archive/samsung-s8/images/customized-rom-16.png)


# PIT OUTPUT

     Heimdall v1.4.2

     Copyright (c) 2010-2017 Benjamin Dobell, Glass Echidna
     http://www.glassechidna.com.au/

     This software is provided free of charge. Copying and redistribution is
     encouraged.

     If you appreciate this software and you would like to support future
     development please consider donating:
     http://www.glassechidna.com.au/donate/

     Entry Count: 30
     Unknown 1: 1598902083
     Unknown 2: 844251476
     Unknown 3: 21324
     Unknown 4: 14153
     Unknown 5: 12852
     Unknown 6: 48
     Unknown 7: 4
     Unknown 8: 0


     --- Entry #0 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 80
     Attributes: 2 (STL Read-Only)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 0
     Partition Block Count: 1024
     File Offset (Obsolete): 1
     File Size (Obsolete): 0
     Partition Name: BOOTLOADER
     Flash Filename: sboot.bin
     FOTA Filename: 
     
     
     --- Entry #1 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 90
     Attributes: 2 (STL Read-Only)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 0
     Partition Block Count: 1792
     File Offset (Obsolete): 2
     File Size (Obsolete): 0
     Partition Name: CM
     Flash Filename: cm.bin
     FOTA Filename: 
     
     
     --- Entry #2 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 91
     Attributes: 2 (STL Read-Only)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 1792
     Partition Block Count: 256
     File Offset (Obsolete): 2
     File Size (Obsolete): 0
     Partition Name: ECT
     Flash Filename: ect.bin
     FOTA Filename: 
     
     
     --- Entry #3 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 1
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 6
     Partition Block Count: 1536
     File Offset (Obsolete): 3
     File Size (Obsolete): 0
     Partition Name: CPEFS
     Flash Filename: 
     FOTA Filename: 
     
     
     --- Entry #4 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 70
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 6
     Partition Block Count: 2
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: PIT
     Flash Filename: -
     FOTA Filename: 
     
     
     --- Entry #5 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 71
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 8
     Partition Block Count: 256
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: MD5HDR
     Flash Filename: md5.img
     FOTA Filename: 
     
     
     --- Entry #6 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 1
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 1024
     Partition Block Count: 1024
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: BOTA0
     Flash Filename: -
     FOTA Filename: 
     
     
     --- Entry #7 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 2
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 2048
     Partition Block Count: 1024
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: NA
     Flash Filename: -
     FOTA Filename: 
     
     
     --- Entry #8 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 3
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 3072
     Partition Block Count: 5120
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: EFS
     Flash Filename: efs.img
     FOTA Filename: 
     
     
     --- Entry #9 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 4
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 8192
     Partition Block Count: 2048
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: PARAM
     Flash Filename: param.bin
     FOTA Filename: 
     
     
     --- Entry #10 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 5
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 10240
     Partition Block Count: 2048
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: UP_PARAM
     Flash Filename: up_param.bin
     FOTA Filename: 
     
     
     --- Entry #11 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 6
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 12288
     Partition Block Count: 2048
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: BOTA2
     Flash Filename: -
     FOTA Filename: 
     
     
     --- Entry #12 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 7
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 14336
     Partition Block Count: 10240
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: BOOT
     Flash Filename: boot.img
     FOTA Filename: 
     
     
     --- Entry #13 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 8
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 24576
     Partition Block Count: 11776
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: RECOVERY
     Flash Filename: recovery.img
     FOTA Filename: 
     
     
     --- Entry #14 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 9
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 36352
     Partition Block Count: 2048
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: BOTA1
     Flash Filename: -
     FOTA Filename: 
     
     
     --- Entry #15 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 10
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 38400
     Partition Block Count: 10752
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: RADIO
     Flash Filename: modem.bin
     FOTA Filename: 
     
     
     --- Entry #16 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 11
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 49152
     Partition Block Count: 256
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: TOMBSTONES
     Flash Filename: tombstones.img
     FOTA Filename: 
     
     
     --- Entry #17 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 12
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 49408
     Partition Block Count: 256
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: DNT
     Flash Filename: dnt.ssw
     FOTA Filename: 
     
     
     --- Entry #18 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 13
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 49664
     Partition Block Count: 128
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: PERSISTENT
     Flash Filename: 
     FOTA Filename: 
     
     
     --- Entry #19 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 14
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 49792
     Partition Block Count: 256
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: MISC
     Flash Filename: 
     FOTA Filename: 
     
     
     --- Entry #20 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 15
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 50048
     Partition Block Count: 1024
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: STEADY
     Flash Filename: steady.bin
     FOTA Filename: 
     
     
     --- Entry #21 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 16
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 51072
     Partition Block Count: 4096
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: KEYREFUGE
     Flash Filename: 
     FOTA Filename: 
     
     
     --- Entry #22 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 17
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 55168
     Partition Block Count: 1113600
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: SYSTEM
     Flash Filename: system.img
     FOTA Filename: 
     
     
     --- Entry #23 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 18
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 1168768
     Partition Block Count: 128000
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: CACHE
     Flash Filename: cache.img
     FOTA Filename: 
     
     
     --- Entry #24 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 19
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 1296768
     Partition Block Count: 2560
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: HIDDEN
     Flash Filename: hidden.img
     FOTA Filename: 
     
     
     --- Entry #25 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 20
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 1299328
     Partition Block Count: 12800
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: OMR
     Flash Filename: omr.img
     FOTA Filename: 
     
     
     --- Entry #26 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 21
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 1312128
     Partition Block Count: 1280
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: CP_DEBUG
     Flash Filename: modem_debug.bin
     FOTA Filename: 
     
     
     --- Entry #27 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 22
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 1313408
     Partition Block Count: 5120
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: NAD_FW
     Flash Filename: nad_fw.bin
     FOTA Filename: 
     
     
     --- Entry #28 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 23
     Attributes: 5 (Read/Write)
     Update Attributes: 1 (FOTA)
     Partition Block Size/Offset: 1318528
     Partition Block Count: 256
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: NAD_REFER
     Flash Filename: nad_refer.bin
     FOTA Filename: 
     
     
     --- Entry #29 ---
     Binary Type: 0 (AP)
     Device Type: 8 (Unknown)
     Identifier: 24
     Attributes: 5 (Read/Write)
     Update Attributes: 5 (FOTA)
     Partition Block Size/Offset: 1318784
     Partition Block Count: 0
     File Offset (Obsolete): 0
     File Size (Obsolete): 0
     Partition Name: USERDATA
     Flash Filename: userdata.img
     FOTA Filename: remained

### Enjoy your fully unlocked Samsung GALAXY S8 !

Ahwell, if it's not clear enough already you must flash the device back to the stock rom after all settings has been done. Of course. 

###### Put it all together to get something looking similar to 
    
    heimdall flash --pit mydevice.pit 
    --ABOOT aboot.mbn \
    --BOOT boot.img \
    --CACHE cache.img.ext4 \
    --MODEM NON-HLOS.bin \
    --RECOVERY recovery.img \
    --RPM rpm.mbn \
    --SBL2 sbl2.mbn \
    --SBL3 sbl3.mbn \
     --SYSTEM system.img.ext4 \
-    -TZ tz.mbn

###### For windows users, just load the .tar files into AP, BL and the other fields and just hit "start" and you are fine.

Stock roms can be found here: https://www.sammobile.com/firmwares/

A tip for all who don't wanna pay for better speeds, then check the source code and find the zip file and you will be able to download the roms with full speed without paying a cent. The .zip is there, you have to think, you will find it. 

#### When You See It You'll Sh*t Bricks, I Promise ;-)

##### Thanks to my friends that gave me this opportunity to play with the Samsung Galaxy S8 ! Of course i unlocked the device for free, you know who you are..

Over And Out. 

Have fun.

// wuseman
