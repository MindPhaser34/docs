# Flash xiaomi.eu ROM (macOS)

In this article, I will show you how I flashed xiaomi.eu ROM with MIUI 14(or HyperOS) to my new device - Xiaomi Mi 13 Ultra. But I think this guide is suitable for owners of other models with Snapdragon Gen 1/2. 

## 1. Unlock bootloader

It's hardest step of whole manual, because official tool for flash ROMs properly works only on Windows OS! Latest version for macos user was released more than 2 years ago and could be found here, but it doesn't work well for new version of macOS:
https://github.com/francescotescari/XiaoMiToolV2

You could find some actual manuals from users in this thread: https://forum.xda-developers.com/t/tool-win-lin-mac-miunlocktool-unlock-bootloader-of-xiaomi-devices-on-mac-linux.3782444/post-85932539

Finally, if you cant find any solution, just run Virtual machine with Windows (virtaulbox, parallels, etc)  and use this unlocker https://en.miui.com/unlock/index.html

Wait for unlock.

#### So, before go ahead, you should do one IMPORTANT thing -  Put this song in the background! :)
https://www.youtube.com/watch?v=jC2ZY2loo74


## 2. Prepare environment

Download latest ROM version: https://sourceforge.net/projects/xiaomi-eu-multilang-miui-roms/files/xiaomi.eu/

Download platform tools and unpack: https://dl.google.com/android/repository/platform-tools-latest-darwin.zip

Download latest TWRP version for device (ishtar), unpack, rename img-file to **recovery.img** and move to folder with platform tools: https://sourceforge.net/projects/recovery-for-xiaomi-devices/files/ishtar/

Enable USB debugging: 
- Settings > My Device > Detailed info & spec. Then click on 'MIUI version' 7 times to enable Developer Options.
- Go to Setting > Additional Settings > Developer options. Switch on "Developer options" and "USB debugging".

## 3. Flash recovery (TWRP)

It's very easy. Boot your device in fastboot mode:
- Turn off the Mi phone completely.
- On the switched off smartphone, press the power and volume down buttons simultaneously.
- Keep them pressed until orange text FASTBOOT appears on a black background.

 Plug in your device and go to the folder with platform tools. To be sure that your device is correctly recognized type in terminal:
```
./fastboot devices -l
```

You will see string with the model of your device. Let's flash TWRP.

```
./fastboot flash recovery_ab recovery.img
./fastboot reboot recovery
```

Then your device will boot to the new recovery.

## 4. Flash xiaomi.eu ROM

- Check this link if you need to change language: https://xiaomi.eu/community/attachments/bez-n%C3%A1zvu-1-png.42793/
- Clear data: Wipe > Format Data
- Mount device to OS: Mount > USB-storage
- Copy ROM: On macOS copy your zip-file with ROM to the internal storage of device via any tools like this https://www.android.com/filetransfer/
- Flash ROM: Install > Select ROM file > Install Image > Reboot (select current partition)

Profit!

## (Bonus) Flash ROMs via Fastboot
You could flash any other ROMs (may be official) without flash TWRP recovery. 
- Download ROM for fastboot version and extract (Latest HyperOS Official ROMs: https://xiaomifirmwareupdater.com/hyperos/ishtar/) 
- Extract it to folder with fastboot
- Boot your device in fastboot mode as in step 3.

The you have next options:

Flash the ROM and erase all user data:
```
./flash_all.sh
```
for new versions (replace "*" is your OS):
```
*_fastboot_first_install_with_data_format.sh
or
*_install_and_format_data.sh
```


Flash the ROM and preserve/save all user data:
```
./flash_all_except_storage.sh
```
for new versions:
```
*_install_upgrade.sh
or
*_fastboot_update_rom.sh
```


Flash the ROM, erase all user data, and lock the bootloader:
```
./flash_all_lock.sh
```
Done.


## PS.
If you have any reason to restore stock recovery, you could do this:
- Download latest official ROM from here [https://xiaomifirmwareupdater.com/miui/](https://xmfirmwareupdater.com/hyperos)
- Unpack it and copy **recovery.img** to platform-tools folder with fastboot
- Flash it as TWRP:
```
./fastboot flash recovery_ab recovery.img
./fastboot reboot recovery
```

Done.
