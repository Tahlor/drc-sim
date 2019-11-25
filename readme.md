DRC Sim Server
---

# EASY INSTRUCTIONS

This is working for me on Ubuntu 18.04. Install server:

    sudo ./install.sh

Backup network config: `sudo cp /etc/NetworkManager/NetworkManager.conf /etc/NetworkManager/NetworkManagerBackup.conf`

* Push sync button
* Run server: `sudo drc-sim-backend`
* Choose interface (e.g. `w1p1s0`)
* Click "Get Key" tab on GUI
* Type in card suit pattern (spades, hearts, clubs, diamonds) 
* Click "Run Server" tab on GUI, with the following settings:
	- Connect to Wii Network
	- WiiU Interface: wlp1s0
	- Normal Interface: lo
	- Region: NA

At some point, the application may change something to be "unmanaged". 
This will temporarily destroy your ability to connect to regular WiFi networks. 
Just replace the `NetworkManager.conf` file with your backup and restart the service (described below)
or your computer.

# Client
Install the Android client from the Play Store OR Desktop version:

Install java 8:
`sudo apt install openjdk-8-jdk`

Find the path to where that installed (e.g. `/usr/lib/jvm/java-8-openjdk-amd64/bin/java`)
    
    alias java8=/usr/lib/jvm/java-8-openjdk-amd64/bin/java 
    
Now run using JAVA 8, `java8 -jar drc-sim-client-2.0.jar`

Once running, go to the main screen, and have it search for the WiiU (should be at 192.168.1.11 automatically if running from the same computer as the server).

# Restore Internet Connectivity to Computer When Done
	
	sudo gedit /etc/NetworkManager/NetworkManager.conf

Restore from backup or comment out the `unmanaged-devices` portion:
    
    #unmanaged-devices=mac:a4:34:d9:1d:b1:95
   
This is the MAC address for `w1p1s0`.

Now restart the network service:

    sudo service network-manager restart

	# OTHER COMMANDS 
	sudo ifconfig wlp1s0 down
	sudo iwconfig wlp1s0 mode managed
	sudo ifconfig wlp1s0 up




Stable: [![Build Status](https://travis-ci.org/rolandoislas/drc-sim.svg?branch=master)](https://travis-ci.org/rolandoislas/drc-sim)
Dev: [![Build Status](https://travis-ci.org/rolandoislas/drc-sim.svg?branch=develop)](https://travis-ci.org/rolandoislas/drc-sim)

DRC Sim Server is a utility for pairing a computer to a Wii U to emulate a gamepad.

It needs a [client] for full functionality.

See the [wiki] for more info.

# Installation

[Installation instructions] are available on the wiki.

# Credits

[drc-sim] \(original\) by [memahaxx]
- The original Python codebase

[libdrc documentation] by memahaxx
- Gamepad and Wii U software and hardware details

[drc-sim-keyboard] by justjake
- The readme that got me set up initially

# Additional Software

[wpa_supplicant] modified by memahaxx

[drc_sim_c] drc-sim rewritten in C++

[netifaces] Python network interfaces library

[pexpect] Python process interaction library



[drc-sim]: https://bitbucket.org/memahaxx/drc-sim
[drc-sim-keyboard]: https://github.com/justjake/drc-sim-keyboard
[Installation instructions]: https://github.com/rolandoislas/drc-sim/wiki/Install
[client]: https://github.com/rolandoislas/drc-sim-client/wiki/Home
[wiki]: https://github.com/rolandoislas/drc-sim/wiki/Home
[wpa_supplicant]: https://github.com/rolandoislas/drc-hostap
[drc_sim_c]: https://github.com/rolandoislas/drc-sim-c
[memahaxx]: https://bitbucket.org/memahaxx/
[libdrc documentation]: http://libdrc.org/docs/index.html
[netifaces]: https://pypi.python.org/pypi/netifaces
[pexpect]: https://pypi.python.org/pypi/pexpect