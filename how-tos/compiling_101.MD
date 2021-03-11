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

## ELF manipulation:
``` bash
# Segments info (readelf is architecture independent):
readelf -s

# Disassemble binary executable (objdump is architecture dependent):
objdump -d <path to elf file>

# Strip all labels inside binary:
strip --strip-unneeded <path to elf file>
```

## Debug program:
* Set flags in cmake:
``` bash
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O0")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0")
```
* Build program with edited cmake
* Run program with gdb:
``` bash
gdb --args <Run program command>
```
* Inside gdb commands:
``` bash
# Start execution:
run

# Show more info about crash:
bt

# Quit:
quit
```

## Debug for memory leaks:
``` bash
valgrind --leak-check=full <Run program command>
# On end valgrind will print all allocations and frees that program did and stack trace where not deallocated malloc happened
```

