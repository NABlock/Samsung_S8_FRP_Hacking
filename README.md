# Samsung_S8_FRP_Hacking
    Bypass Factory Reset Protection on any Samsung Galaxy S8 model on Android 7.0 Nougat or later.

    settings put secure touch_exploration_enabled 1 
    settings put secure wifi_wwsm_patch_remove_sns_menu_from_settings 1
    am start -n com.android.settings/.DevelopmentSettings
    settings put secure send_action_app_error 0
    settings put secure nfc_payment_foreground 0 
    settings put secure bootstartup_status 1
    am start -a android.intent.action.VIEW -d https://nr1.nu com.android.chrome
    
# Check all settings with settings list secure
### List settings

    settings list globaL 

#### Add users when device is locked:

    settings put global add_users_when_locked 1
##### No reason to use mobile data during hacking

    settings put global mobile_data 0
##### We want to install apps to SD since otherwise shit gets protected under encryption, better to avoid this during hacking time


    settings put global add_users_when_locked force_allow_on_external 1 
##### During hacking period, we want all silent  (paranoid? ;))

    settings put global charging_sounds_enabled 0

##### Turn on bluetooth: 

    settings put global bluetooth_on 1
    
##### No reasons for count boot times:
   
    settings put global boot_count 0
    
### Pull all pre-installed applications

    adb pull /system/priv-app/ .
    adb pull /system/app/ .

### Install heimdall
    echo -e "# Heimdall (Flashtool for Sasmung Devices)\napp-mobilephone/heimdall qt5" >> /etc/portage/package.use/use
    emerge --ask app-mobilephone/heimdall

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
###### Go found a rom on the net

### AFter flash has been done, device will reboot, here is some pics how it should look a like: 

# Once booted into FACTORY BINARY, see picture below, here is some hidden tips and tricks from myself ;-)



### Open notification bar: 

#### Its not possible to expand notification bar without touchscreen but with this trick it gonna work and you will have access to all settings by press in upper right corner on the setting icon;)

#### List settings
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

    adb shell content insert --uri content://settings/secure --bind name:s:location_previous_mode  --bind value:s:0

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

    adb shell content insert --uri content://settings/secure --bind name:s:lockscreen.disabled  --bind value:s:1

##### Enable max brightness (Default: 72)

     adb shell content insert --uri content://settings/secure --bind name:s:brightness_pms_marker_screen  --bind value:s:255



##### Expand the notifications wich is hidden and disabled by touch screen:

     adb shell cmd statusbar expand-notifications 



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



##### Thanks to my friends that gave me this possibility to play with her Samsung Galaxy S8 ! 

Happy hacking

##### wuseman
