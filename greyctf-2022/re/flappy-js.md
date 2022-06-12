# flappy-js

## RE - 50 pts (212 Solves)

Are you a pro gamer? Can you get a score of 31337 in this game?

(flag format is greyctf{...} because I made a mistake :p)

http://challs.nusgreyhats.org:10529/

# Solution

git gud lol

Exploring the site's JavaScript files we find `clumsy-min.js`. This seems like a very important file upon inspection, where we can clearly see variables like `score`, `steps` etc.

In fact, the first line already tells us that the game data has the following information:

``` js
data:{
    score:0,
    steps:0,
    start:!1,
    newHiScore:!1,
    muted:!1
}
```

And since the challenge needs us to reach 31337, we can try to change the `steps` to reach this number. In order to do so, we can execute code in the Console, which we can reach from the Developer Tools (or pressing `Ctrl + Shift + J` on Chrome, or `Ctrl + Shift + K` on Firefox).

Then, to modify the variable, we will need to modify `game.data.steps`. So, run `game.data.steps = 31337`. However, if the game isn't in progress, the `steps` will be reset once the game is started. Thus, make sure to start the game first, and then run the line.

Once the game is running and we have set `game.data.steps = 31337`, the game should display the flag `greyctf{5uch_4_pr0_g4m3r}`.

## Alternatively...

Digging around more in the `clumsy-min.js`, we can search for `grey` and we find this one part where we see `"greyctf{"+this.flag+"}"`. Search again for `this.flag`, we find one match where `this.flag=genFlag()`.

If we just run `genFlag()` in the Console, we see that it outputs `5uch_4_pr0_g4m3r`. Combine this with the `"greyctf{"` and close it with `"}"` to get the complete flag, `greyctf{5uch_4_pr0_g4m3r}`.

# Flag

`greyctf{5uch_4_pr0_g4m3r}`