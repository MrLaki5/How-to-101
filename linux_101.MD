## Some basic linux commands:

* Open nano editor with line numbering:
``` bash
nano -c <file path>
```

* Read logs live:
``` bash
tail -f <log path>
```

* Search through command history:
``` bash
CTRL + R # In terminal, after search if there are more similart commands, iteration is posible with pressing CTRL + R again
```

* New termianl tab: 
``` bash
CTRL + SHIFT + T
```

* Third party solutions:
``` bash
tig # Git tree
terminator # CLI with extra options to split h and w.
```

* Tig all branches:
``` bash
tig --all
```

* Search through filesystem:
``` bash
find <root_path> -iname "<file_name_reg>"
```

* Check size on disk of filesystem:
``` bash
df -h
```

* Recursive all folders to depth (-d) and their sizes:
``` bash
du -h /path/to/directory -d 1
```

* Checks remotes for git repo:
``` bash
git remote -v
```

* Go back to previous dir location:
``` bash
cd -
```