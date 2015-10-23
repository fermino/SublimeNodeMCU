# Sublime Node MCU Uploader

A Sublime3 plugin written in Python3 that allows you to upload the current file (usually some lua code, ex init.lua) to a NodeMCU (ESP8266) microcontroller by simply pressing the F7 button.
This is almost entirely based on the original work posted on the esp8266.com forums by Markus Gritschat (http://www.esp8266.com/viewtopic.php?f=22&t=1026). I downloaded the script, but I was determined to make it work with Python3 and overall do a good refactoring. It has worked well for me, submit an issue if you have any problems installing or using it.

# How it works (under the hood)
This script takes a few steps to upload your file...
1. Establish a Serial Connection with the NodeMCU based on the port set in the header
2. Sends a small shell script to the NodeMCU which it immediately runs. This script receives serial data on the COM port and writes it to the file on the NodeMCU. I'm not sure if it could be done differently, but I found this method pretty clever, and it works.
3. Reads the file into a buffer and chunks it over the COM port to the NodeMCU, checking for an ACK every chunk_size bytes
4. And, if enabled, sends a command to the Node MCU to run that file

# Example Console Output
```
Uploading to NodeMCU...
Opening serial port COM4:9600...ok!
Reset...ok!
Sending Save Command to NodeMCU....ok!
Reading E:\home\kevin\Projects\Pursuant\GarageMCU\GarageMCU.lua into memory...ok!
  7 % 15 % 23 % 31 % 38 % 46 % 54 % 62 % 70 % 77 % 85 % 93 %
[Finished in 6.8s]
```