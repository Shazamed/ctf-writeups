# Too Fast

## Web - 50 pts (92 Solves)

Something went by too quickly!

http://challs.nusgreyhats.org:14004/

# Solution

Opening the page, we notice the following comments in navbar:

```
<li><a href="#"><span class="glyphicon glyphicon-user"></span> Your Account</a></li> // to do soon
<li><a href="#"><span class="glyphicon glyphicon-shopping-cart"></span> Cart</a></li> // this too and also our special portal
```

This sort of hints to us to find another page.

Either way, we run a directory brute force on the webpage. Using [`dirb`](https://www.kali.org/tools/dirb/) to scan the web server, we notice that it found `admin.php` to return a `302 HTTP` response. Accessing `http://challs.nusgreyhats.org:14004/admin.php` will quickly redirect us back to `http://challs.nusgreyhats.org:14004/index.php`, indicating to us that we are on the right path as hinted by the challenge title and the description.

To retrieve the content of `/admin.php` while avoiding the redirect, we can simply use `curl http://challs.nusgreyhats.org:14004/admin.php`, which returns to us:

```
<p><span style='color: #ffffff;'>grey{why_15_17_571LL_ruNn1n_4Pn39Mq3CQ7VyGrP}</span></p>
```

## Alternatively...

An alternative solution is to just access `http://challs.nusgreyhats.org:14004/README.md`, which simply lists a few very helpful pieces of info:

```
# t00 f4st

### Challenge Details
a challenge testing on [Execution After Redirect](https://owasp.org/www-community/attacks/Execution_After_Redirect_(EAR))

### Key Concepts
- enumerate web
- learn how to abuse Execution After Redirect

### Solution
cURL or figure ways to view the flag before being redirected. Use Burp maybe.

### Learning Objectives
same as key concept

### Flag
grey{why_15_17_571LL_ruNn1n_4Pn39Mq3CQ7VyGrP}
```

# Flag

`grey{why_15_17_571LL_ruNn1n_4Pn39Mq3CQ7VyGrP}`