---
title: Setting up Android x86 on Oracle VBox for Burpsuite
view: 2
header:
  caption: ""
  image: ""
date: 2020-07-07T13:00:57.002Z
draft: true
featured: true
image:
  preview_only: true
  filename: featured.jpeg
---


![](https://cdn-images-1.medium.com/max/1200/0*09TQIlQpCUJQJmsg)

Photo by [Pathum Danthanarayana](https://unsplash.com/@pathum_danthanarayana?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Security Analysis of the Android Phones usually requires a rooted phone along with custom requirements for certain conditions like a minimum Android tier, certain Hardware, peripherals, etc. This problem is easily solvable by using the Android emulators like Genymotion. However, they usually have shortcomings, eg, Genymotion currently does not support BlueTooth integration. For a recent task, I needed to analyze an app that required Bluetooth along with a newer Android, however, since most of the emulators did not support Bluetooth and I did not have a rooted newer version Android phone, I had to find a suitable emulator. The Android x86 emulator best suited my needs. Android x86 emulator is:

* Rooted off the shelf
* Supports Bluetooth
* Available for almost all Android Versions

I had to use it with the burp suite on Windows 10 using Oracle Virtual Box. I had to troubleshoot during the process, that is why I am compiling my process here so that one can set it up with relative ease.

First, you need to install it. You have two options:

* Getting iso file from [here](https://www.android-x86.org/).
* Getting VirtualBox VDI from [here](https://www.osboxes.org/android-x86/)(recommended).

Install the VDI for Android (of your choice, virtual wifi support is present in Android 7+ Android x86) After that follow these steps:

* Create a new VM in Oracle VirtualBox.
* Select its type as Linux.
* Choose Other(32 bit) as the version if you have installed 32-bit VDI, otherwise choose Other(64 bit).
* Assign >=2GB of RAM.
* For the hard drive, select Use an existing virtual hard disk file and select the downloaded VDI file.

After the new VM has been set up, go to settings, and do the following:

* Assign >1 processor to the VM.
* Select Mouse as the pointing device in the System>Motherboard settings.
* In Display>Screen select VBoxSVGA as the Graphics Controller and enable 3D acceleration.

The upcoming steps would allow us to use BlueTooth in our emulator. For that,

* Go to Settings>Serial Ports and in port 1, check enable the serial port.

Now, go to the Windows Device Manager, go to Bluetooth, and open the properties of your Bluetooth card. Go into Details, and select HardwareID. Note the Product ID of the device written after PID in detail.

Run the Android x86 emulator. Once it is opened, open Devices>USB and select the device having the same Product ID as your Bluetooth card.

After this, you can use BlueTooth in the emulator just like on your physical device.

To Check IP Address of the emulator press Alt+f1 to open the terminal in emulator and type ipconfig, then note the ipv4 address of eth0.

After this step, you can set up ADB, and Burpsuite as usual.

#### **Important Resources**

Following resources were used mainly for troubleshooting:

* [How to Install Android on Virtualbox — YouTube](https://www.youtube.com/watch?v=JQc6VXuwlWk)
* [Bluetooth in Android x86 on Virtualbox](https://stackoverflow.com/questions/17806386/bluetooth-in-android-x86-on-virtualbox)
* [Setting up an Android Hacking Environment](https://init6.me/android-hacking-environment/) (Helpful for older Android x86 versions)