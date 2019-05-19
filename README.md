# Samsung_S8_FRP_Hacking
Bypass Factory Reset Protection on any Samsung Galaxy S8 model on Android 7.0 Nougat or later.

# Install heimdall
echo -e "# Heimdall (Flashtool for Sasmung Devices)\napp-mobilephone/heimdall qt5" >> /etc/portage/package.use/use
emerge --ask app-mobilephone/heimdall

# Detect Device:
heimdall detect

# Download PIT:
heimdall download-pit --no-reboot --output mydevice.pit

# Print PIT:
heimdall print-pit --no-reboot --file mydevice.pit

# Boot device into flash mode:
Poweroff device
Press vol dn+powerbutton

# Flash your device with the customized rom 
# Go found a rom on the net

# AFter flash has been done, device will reboot, here is some pics how it should look a like: 
