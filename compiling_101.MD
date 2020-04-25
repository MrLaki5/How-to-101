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
./test
```