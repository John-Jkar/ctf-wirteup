# iuesbitaipsi
475
**forensics easy**

Author: mrbgd

ayay uat is iuor taip for iuesbi?

# Method of solve
We were given a pcap file for analysing usb forensics. Using tshark I first looked for usb.hid from the file using
~~~
tshark -r nullctf.pcapng -Y "usb.transfer_type == 0x01 && usbhid.data" -T fields -e usbhid.data
~~~
then I wrote a python script to decode the keystrokes
~~~
import sys

KEYS = {
    0x04:"a",0x05:"b",0x06:"c",0x07:"d",0x08:"e",0x09:"f",0x0a:"g",0x0b:"h",
    0x0c:"i",0x0d:"j",0x0e:"k",0x0f:"l",0x10:"m",0x11:"n",0x12:"o",0x13:"p",
    0x14:"q",0x15:"r",0x16:"s",0x17:"t",0x18:"u",0x19:"v",0x1a:"w",0x1b:"x",
    0x1c:"y",0x1d:"z",0x1e:"1",0x1f:"2",0x20:"3",0x21:"4",0x22:"5",0x23:"6",
    0x24:"7",0x25:"8",0x26:"9",0x27:"0",
    0x2c:" ",0x28:"\n",0x2d:"-",0x2e:"=",0x2f:"[",0x30:"]",0x33:";",0x34:"'",0x36:",",0x37:".",0x38:"/"
}

SHIFT_KEYS = {
    "1":"!", "2":"@", "3":"#", "4":"$", "5":"%", "6":"^", "7":"&", "8":"*", "9":"(", "0":")",
    "-":"_", "=":"+", "[":"{", "]":"}", ";":":", "'":'"', ",":"<", ".":">", "/":"?"
}

for line in sys.stdin:
    hexbytes = bytes.fromhex(line.strip())
    modifier = hexbytes[0]
    code = hexbytes[2]
    if code in KEYS:
        char = KEYS[code]
        if modifier & 0x22:  # Shift pressed (left or right)
            char = SHIFT_KEYS.get(char, char.upper())
        print(char, end="")
~~~
After I used tshark with the script to get the flag.
~~~
tshark -r nullctf.pcapng -Y "usb.transfer_type == 0x01 && usbhid.data" -T fields -e usbhid.data | python3 decode.py 
~~~
