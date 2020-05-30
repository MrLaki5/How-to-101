## Create share library:
``` bash
# Build object for shared library
g++ -c -fpic foo.c

# Create shared library
g++ -shared -o libfoo.so foo.o

# Build with shared library
g++ -L/home/username/<path to lib folder> -o test main.c -lfoo

# Run
export LD_LIBRARY_PATH=/home/username/<path to lib folder>:$LD_LIBRARY_PATH
# NOTE: linker will go path by path through LD_LIBRARY_PATH untill it finds first reference for specific shared library. 
# So if same lib is placed in multiple paths first found will be used.
./test
```

## Dynamic library check: 
``` bash
# Check shared libraries for specific bin:
ldd <path to bin>

# If there are some undefined symbols (eg: _Z22CxxxPxxxExxxPxxxR6CDBManRKSsRSt6vectorISsSaISsEE, this will give you whats mangled:
c++filt <undefined symbol>

# List symbols used in shared lib:
nm  [-C] <path to shared lib>
# -C: will show damaged symbols
```

## Disassemble binary executable:
``` bash
objdump -d <path to elf file>
```
