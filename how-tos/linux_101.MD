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
nethogs # Network traffic
terminator # CLI with extra options to split h and w.
timeshift # mechanism for saving state's of current system (backups if something goes wrong)
```

* Tig all branches:
``` bash
tig --all
```

* Search through filesystem for specific file:
``` bash
find <root_path> -iname "<file_name_reg>"
```

* Search through filesystem for specific text in files:
``` bash
grep -rnw '<root_path>' -e '<text_to_find>'
# -n: prints line number where text occured
# -r|R: recursive
# -w: match the whole word
# -l: for giving just names of matching files
# 2> /dev/null: move error out, so permission denied messages are not shown
```

* Search through filesystem for specific text in ELF:
``` bash
grep -Hrin "haveImageReader" <path_to_lpdnn>
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

* Get process started with specific command:
``` bash
ps aux | grep -i "<part of command>"
```

* Kill process:
``` bash
# Lite version
kill <pid>

# Hard version
kill -Kill <pid>
```

* GRUB boot package loader (eg. kernel siwtching):
``` bash
# Modify grub configuration:
sudo nano /etc/default/grub
sudo update-grub

# Open grub loader on boot time:
# Press and hold <shift key> while booting, in case of UEFI press and hold <escape key>
```
