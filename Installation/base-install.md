Before we begin, I hope you have already created a bootable USB drive with the Arch ISO.

Verifying the boot environment
What does this mean? We are checking whether your device is set to UEFI or BIOS mode. There are slight differences in the installation process for both. There is a easy way to check it. That is during the initial boot. If you got greeted with a menu like this,

image

As you can see, 'UEFI' is clearly written on that image. So, the system is booted into UEFI mode. This is an easy way to recognise which mode your system has booted into without using any commands. Or run this command:

cat /sys/firmware/efi/fw_platform_size
//if it returns 64, then you are booted into UEFI mode.
//if it returns "no file exist", then you are booted into BIOS mode.
Connecting to Internet
Personally, I recommend using an Ethernet connection when setting up Arch Linux for the first time. Things can get a bit tricky when setting up Wi-Fi.

For ethernet, just plug it in.

To use Wi-Fi, you will need to use a utility called 'iwctl'.

$iwctl  //to get into the interactive prompt

device list //To list out your adapter name

station name scan //This will initialize scanning and replace name with your adapter name

station name get-networks //List out the available wifi names

station name connect SSID //To connect to your Wi-FI
After that, check if you're actually connected to the internet:

ping www.archlinux.org
If it responds, internet is working.

Press Ctrl+C to stop.