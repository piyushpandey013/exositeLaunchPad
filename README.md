Exosite on MSP430F5529 LaunchPad for Energia and CCS
====================================================

Exosite Energia Library for CC3000

This library allows you to quickly and easily connect your LaunchPad project to Exosite's Data Platform in the cloud. It connects your project using a LaunchPad and CC3000 BoosterPack. See the examples folder for a WiFi example.

Note: A free account on exosite portals is required: https://ti.exosite.com

License is BSD, Copyright 2013, Exosite LLC (see LICENSE file)

Tested with Energia 0101E0011

Installing
==========
The easiest way to install this library is to simply clone this repo straight to your libraries folder.

```
cd ~/hardware/msp430/libraries
git clone https://github.com/awhitehead/exositeEnergia.git Exosite
```

If you would rather not use the command line or you don't have git installed, click the download button on the right hand side of this page and choose to open the ZIP. Copy the contained folder to your Energia IDE's libraries folder.

Note: You will need to restart the Energia IDE after installing the library.

NOTE: Interface, Migration, and Release Info below is referenced from the Arudino ported library at https://github.com/exosite-garage/ (as of 14JAN2014)

Interface
=========
```c
boolean Exosite::writeRead(char* writeString, char* readString, char** returnString)
```

```c
boolean Exosite::writeRead(String writeString, String readString, String &returnString)
```

`writeString`: This sets the values to write to certain datasources. eg. "alias3=value3&alias4=value4"

`readString`: This selects which datasources to read by their alias. eg. "alias1&alias2"

`returnstring`: This is the string returned with the values requested in `readString`. eg. "alias1=value1&alias2=value2"


Migration from V1
=================
Version 2 no longer sets up the ethernet shield for you. In your code you'll need to replace `Exosite exosite(&Ethernet, macData, cikData);` with 

```
class EthernetClient client;
Exosite exosite(cikData, &client);
```
You will also need to remove `exosite.init();` and add `Ethernet.begin(macData);` to your setup() function.

Release Info
============
**v2.1.1 - Release 2013-11-04**
 - Removed depreciated 'readWrite' method to reduce confusion. 'readFromCloud' and 'sendToCloud' still supported.

**v2.1 - Release 2013-11-01**
 - Changed 'readWrite' to 'writeRead' to reflect parameter order and platform operation order.
 - Added User-Agent String
 - Added client->flush() just before sending HTTP packet, just in case we received something

**v2.0 - Release 2013-10-18**
 - Simplified interface to use character strings or Arduino Strings instead of arrays of character arrays. User must now URL encode and decode their own data.
 - Made compatible with Arduino WiFi shield (and anything that similarly subclasses the Client class).
 - Updated examples to use new interface.

**v1.1 - Release 2013-07-29**
 - Major rewrite to both read and write multiple datasources in one HTTP call.
 - Removed all use of Strings due to stability issues (except for manipulating string object passed to existing functions).
 - Existing `sendToCloud()` and `readFromCloud()` changed to use new call internally. External Interface Unchanged

**v1.0 - Release 2011-06-05**
 - initial version