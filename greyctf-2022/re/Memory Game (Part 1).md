# Memory Game (Part 1)

## RE - 50 pts (156 Solves)

Here's a fun game to destress.

Do you know where the image assets are stored? I've made a nice drawing for you.

Files: memory-game.apk

# Solution

We are given an `.apk` file and are told to find a drawing in the image assets folder. We would like to take a look inside this `.apk` file, and one easy way to do so is to simply change the extension from `.apk` to `.zip`, and from here we can extract the files.

Looking inside the extracted files, we see 3 folders, `assets`, `META-INF`, and `res`. Even if you don't have much background knowledge about where image assets are stored, we can quickly check the contents of these 3 folders, and find that the `res` folder has a lot of `.png` files, so it is most likely within this `res` folder.

Now we just scroll through the images (makes it easier if you use Windows File Explorer Large Icons) and find a very peculiar white image, with some black text going across it. Opening up `iA.png`, we find the flag, `grey{th1s_1s_dr4w4bl3_bu7_e4s13r_t0_7yp3}`.

![iA.png](./Memory%20Game%20(Part%201)/iA.png)

# Flag

`grey{th1s_1s_dr4w4bl3_bu7_e4s13r_t0_7yp3}`