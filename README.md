# cascoda-openwrt
This repository contains the OpenWrt source package for the Cascoda SDK.

## Installing the Cascoda SDK
Installing the Cascoda SDK makes the package available in `make menuconfig`, which is the build system configuration interface. 

First, ensure that you have OpenWrt version 19.07.0 or later, otherwise you will have to manually update the cmake tool to make sure you have CMake version 3.13 or newer. This is necessary in order to build the Cascoda SDK.

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

Exit and save configuration.

After building and flashing the image to your device operating on OpenWrt, the following Cascoda applications will be available:
<pre>	
ca-ot-cli-ftd           - A command line interface to the OpenThread stack, acting as a Full Thread Device
ca-ot-cli-mtd           - The OpenThread CLI, acting as a Minimal Thread Device
ca-sniffer              - An example program for sniffing 802.15.4 traffic on a specific channel.
ca-ot-ncp               - Network Co-Processor for interacting with openthread wpantund.
ca-ot-sensordemo-server - A server program able to connect to thread devices and interpret sensor data.
ca-serial-adapter       - A useful program for interacting with a serial application running on baremetal.
ca-evbme-get            - Prints information about connected Cascoda devices
</pre>
