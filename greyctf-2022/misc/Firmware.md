# Firmware

## Misc - 50 pts (104 Solves)

Router firmware is a nice target to start your bug hunting journey. But you have to first understand how the firmware is loaded.

There is always a file in the firmware image that tells the router what services to start. Find this file.

Files: [firmware.img.gz](./Firmware/firmware.img.gz)

# Solution

As hinted in the challenge description, we need to find the file that will start up the system's processes. Some research will reveal that the `/etc` folder is usually the folder containing the system configuration files. Even more research will show that upon booting the system, the `init` daemon will start processes by reading from the `/etc/inittab` file.

Opening the `etc/inittab` file, we see the following:

```
::sysinit:/etc/init.d/rcS S boot
::shutdown:/etc/init.d/rcS K shutdown
::askconsole:/usr/libexec/login.sh

# you found me! grey{inittab_1s_4n_1mp0rt4nt_pl4c3_t0_l00k_4t_wh3n_r3v3rs1ng_f1rmw4r3}
```

## Alternatively...

We can just write a script to look through all the files and see if they contain the string `grey{`.

```python
import os

# recursively search all files and return the file with the string
def search(string):
    for root, dirs, files in os.walk('./1'):
        for file in files:
            content = open(os.path.join(root, file), encoding="utf-8", errors='ignore').read()
            if string in content:
                print(content)
                return os.path.join(root, file)

search('grey{')

# ::sysinit:/etc/init.d/rcS S boot
# ::shutdown:/etc/init.d/rcS K shutdown
# ::askconsole:/usr/libexec/login.sh

# # you found me! grey{inittab_1s_4n_1mp0rt4nt_pl4c3_t0_l00k_4t_wh3n_r3v3rs1ng_f1rmw4r3}
```

# Flag

`grey{inittab_1s_4n_1mp0rt4nt_pl4c3_t0_l00k_4t_wh3n_r3v3rs1ng_f1rmw4r3}`