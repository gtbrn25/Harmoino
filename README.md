This is my first ever Github repository.  Exciting.

I used Claude to update the pkscout/Harmoino repository with some additional features for the Harmony remotes:
- Added SPI ethernet module capability (W5500).  Ethernet provides much more reliable/consistent button presses than my wifi.
- Updated the MQTT topic to be the device name vs the mac address.  Must ensure there are not duplicate device names.
- Added ability to add up to 4 total remotes.  Each must be paired with the same Harmony hub and only the last byte of each address can be different.  I've noticed Harmony hubs typically go in sequence for that last byte, 0A -> 0B -> 0C, etc.  In the defaults file, enter full address for remote_adr (which still follows the pairing process).  Additional remotes can be added by putting the full address in each remote_adr_pipe variable after initializing remote_adr.
- Updated Home Assistant to have sensors for the MQTT Topic (for entering into Node-RED) and each additional pipe address.

This can likely be expanded to
1. Expand MQTT topic to capture which physical remote / pipe address sent the message.  One central Harmoino with remotes in two different rooms with different TVs.
2. Better setting of the additional pipe addresses through Home Assistant.
3. Claude seems to think Pipe 0 and Pipes 1-5 can have completely separate addresses, so it could be possible to have 6 total remotes.  My attempt failed, but I only tried a single code revision.  Don't need this capability yet.


# Harmoino OpenHub for Home Assistant
The primary focus of this fork is a new HomeAssistantHub that combines all the remote discovery and operations from the original into one sketch and automatically creates a device in Home Assistant so that you can use your Harmony remote to control things in Home Assistant.

Please see the wiki pages for details on the hardware setup, software install, and operation.


## Acknowledgements
None of this would have been possible without the work joakimjalden did to reverse engineer the radio signals between the Harmony Hub and the remote.  [Here's the original repository](https://github.com/joakimjalden/Harmoino).  The original readme and code are still here are well.  And here's joakimjalden's original acknowledgements too.

> First, I wish to acknowledge the [Hacking the Harmony RF Remote](https://haukcode.wordpress.com/2015/04/16/hacking-the-harmony-rf-remote/) blog post on Hakan's Coding and Stuff. This post gave me crucial pointers early on, especially with the radio hardware. I can also recommend the discussion thread for helpful information on pairing the Harmony Remote with the Logitech Unifying Receiver on a PC if you are looking for a more software-based solution. Second, the [Simple nRF24L01+ 2.4GHz transceiver demo](https://forum.arduino.cc/t/simple-nrf24l01-2-4ghz-transceiver-demo/405123) by Robin2 was tremendously helpful in getting started with the RF24 library for the Arduino, and it inspired the minimalistic SimpleHub implementation.
