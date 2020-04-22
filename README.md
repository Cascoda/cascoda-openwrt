# cascoda-openwrt
This repository contains the OpenWrt source package for the Cascoda SDK.

## Installing the Cascoda SDK
Installing the Cascoda SDK makes the package available in `make menuconfig`, which is the build system configuration interface. 

First, ensure that you have CMake version 3.13 or newer, as this is necessary to build the Cascoda SDK. 
This can be downloaded from the [CMake Website](https://cmake.org/download/).

Add the Cascoda SDK package as a feed by adding the following line to the `feeds.conf` file:<br />
`src-git cascoda_sdk https://github.com/Cascoda/cascoda-openwrt.git`.

Update the feeds: `$ ./scripts/feeds update -a`

Install the packages from the feeds: `$ ./scripts/feeds install -a`

## Configuring the image using `make menuconfig`
Start the build system configuration interface: `$ make menuconfig`

Include the `cascoda-sdk` package:
1. Go to `Utilities`
2. Hover over `cascoda-sdk`
3. Press the `y` key to include the package

Include the `hidapi` package (this is necessary for the Chili module to be recognised as a USB HID device):
1. Go to `Libraries`
2. Hover over `hidapi`
3. Press the `y` key to include the package

Include the `kmod-usb-hid` package (for the same reason as above):
1. Go to `Kernel modules ---> USB Support`
2. Hover over `kmod-usb-hid`
3. Press the `y` key to include the package

Exit and save configuration.

After building and flashing the image to your device operating on OpenWrt, the following Cascoda applications will be available:
<pre>	
ca-ot-cliapp            - A command line interface to the Openthread stack.
ca-sniffer              - An example program for sniffing 802.15.4 traffic on a specific channel.
ca-ot-ncpapp            - Network Co-Processor for interacting with openthread wpantund.
ca-ot-server-standalone - A server program able to connect to thread devices and interpret sensor data.
ca-serial-adapter       - A useful program for interacting with a serial application running on baremetal.
ca-comm-check           - An application that tests the USB communications link for reliability and speed.
</pre>
