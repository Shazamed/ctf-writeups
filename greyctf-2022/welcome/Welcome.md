# Welcome

## Welcome - 50 pts (360 Solves)

Join our discord server @ https://discord.gg/d9wbXEP2wN

The flag is in #rules

# Solution

As clearly hinted in the challenge description, we have to join the 'discord server'. We have to find this 'discord server', perhaps a OSINT challenge. 

One way of approaching this is by finding more information about this 'ctf' thing. It appears to be run by this weird organisation called ~~nusgreyshats~~ nusgreyhats. We can easily find their website using this common OSINT tool called Goggle.com. They have a 'the team' section on their website, and it seems there are like 24 members or something, so it shouldn't take too long to email them one by 1 for this discord server. They have also kindly listed all the ways to contact them, so we surely must be on the right track! 

Wait it seems like we don't have to do that. Fortunately for us, it seems the challenge author accidentally left a hint to the server! haha they are soooo dumb

Clicking the suspicious link `https://discord.gg/d9wbXEP2wN`, we are suddenly inundated with a splash screen commanding us enter our username. This is most likely a phising attack, trying to steal our credentials and private information.

There is an available exploit here. Instead of entering our real name, we can put in a fake alias to bypass this security authentication screen. Upon proceeding by clicking on the **Continue** button, sometimes we face another round of authentication asking us if "I am human". tbh we have no idea how to get around this so just click some random squares when they pop up.

If you managed to get pass that, you'll reach yet another stage of authentication. Luckily we can use the same exploit and enter in a fake birthday. Since today is actually my birthday, we'll put tomorrow as the birthday.

A popup then demands you to enter an email and password. Again, yet another common phishing attack. Fortunately, there is a bug to exploit here, and can be executed by moving the mouse to outside of the popup and then left-clicking outside of the popup.

Finally we are loaded into this 'discord server'. We are told that the flag is in `#rules`. However, we are unable to find the `#rules` channel. After some digging around, we realise there is the `#🈲-rules` channel instead. This may be a mistake by the challenge authors.

Next, we need to get the content of the `#🈲-rules` channel. Attempting to retrieve this data with `curl https://discord.com/channels/969232688521281606/969232688911360031` returns the following:

```
<!DOCTYPE html>
<html>
  <head>    <meta charset="utf-8" />
    <meta content="width=device-width, initial-scale=1.0, maximum-scale=3.0" name="viewport" />

    <!-- section:seometa -->
    <meta property="og:type" content="website" />
    <meta property="og:site_name" content="Discord" />
    <meta property="og:title" content="Discord - A New Way to Chat with Friends & Communities" />
    <meta
      property="og:description"
      content="Discord is the easiest way to communicate over voice, video, and text.  Chat, hang out, and stay close with your friends and communities." /><meta property="og:image" content="undefined//discord.com/assets/652f40427e1f5186ad54836074898279.png" />    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:site" content="@discord" />
    <meta name="twitter:creator" content="@discord" />
    <!-- endsection --><script nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==">window.GLOBAL_ENV = {
        API_ENDPOINT: '//discord.com/api',
        API_VERSION: 9,
        GATEWAY_ENDPOINT: 'wss://gateway.discord.gg',
        WEBAPP_ENDPOINT: '//discord.com',
        CDN_HOST: 'cdn.discordapp.com',
        ASSET_ENDPOINT: '//discord.com',
        MEDIA_PROXY_ENDPOINT: '//media.discordapp.net',
        WIDGET_ENDPOINT: '//discord.com/widget',
        INVITE_HOST: 'discord.gg',
        GUILD_TEMPLATE_HOST: 'discord.new',
        GIFT_CODE_HOST: 'discord.gift',
        RELEASE_CHANNEL: 'stable',
        MARKETING_ENDPOINT: '//discord.com',
        BRAINTREE_KEY: 'production_5st77rrc_49pp2rp4phym7387',
        STRIPE_KEY: 'pk_live_CUQtlpQUF0vufWpnpUmQvcdi',
        NETWORKING_ENDPOINT: '//router.discordapp.net',
        RTC_LATENCY_ENDPOINT: '//latency.discord.media/rtc',
        ACTIVITY_APPLICATION_HOST: 'discordsays.com',
        PROJECT_ENV: 'production',
        REMOTE_AUTH_ENDPOINT: '//remote-auth-gateway.discord.gg',
        SENTRY_TAGS: {"buildId":"d9eb65241de00577fd05fe6ae3e9193417844d06","buildType":"normal"},
        MIGRATION_SOURCE_ORIGIN: 'https://discordapp.com',
        MIGRATION_DESTINATION_ORIGIN: 'https://discord.com',
        HTML_TIMESTAMP: Date.now(),
        ALGOLIA_KEY: 'aca0d7082e4e63af5ba5917d5e96bed0',
      };</script><script nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==">!function(){if(null!=window.WebSocket){if(function(n){try{var e=localStorage.getItem(n);return null==e?null:JSON.parse(e)}catch(n){return null}}("token")&&!window.__OVERLAY__){var n=null!=window.DiscordNative||null!=window.require?"etf":"json",e=window.GLOBAL_ENV.GATEWAY_ENDPOINT+"/?encoding="+n+"&v="+window.GLOBAL_ENV.API_VERSION+"&compress=zlib-stream";console.log("[FAST CONNECT] connecting to: "+e);var o=new WebSocket(e);o.binaryType="arraybuffer";var t=Date.now(),i={open:!1,identify:!1,gateway:e,messages:[]};o.onopen=function(){console.log("[FAST CONNECT] connected in "+(Date.now()-t)+"ms"),i.open=!0},o.onclose=o.onerror=function(){window._ws=null},o.onmessage=function(n){i.messages.push(n)},window._ws={ws:o,state:i}}}}();</script><link rel="prefetch" as="script" href="/assets/cc8521999cf151dad3fb.js"></link><link rel="prefetch" as="script" href="/assets/b4499d2a6b9046b1b402.js"></link><link rel="prefetch" as="script" href="/assets/4b58fa778cc38e586a72.js"></link><link rel="prefetch" as="script" href="/assets/4b582ee1842099625350.js"></link><link rel="prefetch" as="script" href="/assets/2a6b8d1c4c54837fbc1c.js"></link><link rel="prefetch" as="script" href="/assets/591f9dafb1c84fb4fa70.js"></link><link rel="prefetch" as="script" href="/assets/89c07f6464c4df65e564.js"></link><link rel="prefetch" as="script" href="/assets/4246c68ec807e086f261.js"></link><link rel="prefetch" as="script" href="/assets/2839fc52cff38f4d0ee7.js"></link><link rel="prefetch" as="script" href="/assets/4ba4978bd8a3fc499d46.js"></link><link rel="prefetch" as="script" href="/assets/2ea8e76a2d49de55d2ed.js"></link><link rel="prefetch" as="script" href="/assets/606aa4d52a93b72a6591.js"></link><link rel="prefetch" as="script" href="/assets/446e0e9a0512cf1362dd.js"></link><link rel="prefetch" as="script" href="/assets/548375d0085d53842a3d.js"></link><link rel="prefetch" as="script" href="/assets/49c74496cfc5835955b6.js"></link><link rel="prefetch" as="script" href="/assets/c8919ff4992e51ead916.js"></link><link rel="prefetch" as="script" href="/assets/53f56d57c8170d14b5fc.js"></link><link rel="prefetch" as="script" href="/assets/84e72f3a10e9f967f24a.js"></link><link rel="prefetch" as="script" href="/assets/4d5aeab2a9f3265da3e1.js"></link><link rel="prefetch" as="script" href="/assets/6a4d271d26e063c4b4f7.js"></link><link rel="prefetch" as="script" href="/assets/7124453700a3afeff79d.js"></link><link rel="prefetch" as="script" href="/assets/f66cf1e31d786afb147f.js"></link><link rel="prefetch" as="script" href="/assets/4f0f3dfb9830355dc0c4.js"></link><link rel="prefetch" as="script" href="/assets/7d963e768a87b4c17179.js"></link><link rel="prefetch" as="script" href="/assets/ef0cdc0db3be88e70f2c.js"></link><link rel="prefetch" as="script" href="/assets/613465ae3ccf3e86df70.js"></link><link rel="prefetch" as="script" href="/assets/b857e813eb5b9881a085.js"></link><link rel="prefetch" as="script" href="/assets/40fbcd706ee16c96b281.js"></link><link rel="prefetch" as="script" href="/assets/0f24c6bd84d0ef137c75.js"></link><link rel="prefetch" as="script" href="/assets/0d1cb14adfd1c7903b64.js"></link><link rel="prefetch" as="script" href="/assets/b2b987a5b71c9b5a287a.js"></link><link rel="prefetch" as="script" href="/assets/d17199a5e24145fcce41.js"></link><link rel="prefetch" as="script" href="/assets/b9a70c16149b98d13108.js"></link><link rel="prefetch" as="script" href="/assets/139bb67aa47a374ec3e7.js"></link><link rel="prefetch" as="script" href="/assets/47bdd59a25caeb417e46.js"></link><link rel="prefetch" as="script" href="/assets/7dd08041c2cb6478fa51.js"></link><link rel="prefetch" as="script" href="/assets/13d00da694f4981d1aa0.js"></link><link rel="prefetch" as="script" href="/assets/12b4618e291b025f6aa7.js"></link><link rel="stylesheet" href="/assets/40532.6d7d82b952ea79d8edf8.css" integrity="sha256-+1du0AFN9DJlGIjM+D5oC1CSv3e9umIN65+CYqN0VEI= sha512-mtXAD3/GIWgi8Jvtq7ej/uYIdanQchcl4EynKRD4dYzQenewev2wN676lKjwybwGuigVaMByrt9dBV09kVcS7g=="><link rel="icon" href="/assets/ec2c34cadd4b5f4594415127380a85e6.ico" />    <!-- section:title -->
    <title>Discord</title>
    <!-- endsection -->
  <script async nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==" src='/cdn-cgi/bm/cv/669835187/api.js'></script></head>
  <body>
    <div id="app-mount"></div><script nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==">window.__OVERLAY__ = /overlay/.test(location.pathname)</script><script nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==">window.__BILLING_STANDALONE__ = /^\/billing/.test(location.pathname)</script><script src="/assets/d0388e923ab3b6194d90.js" integrity="sha256-WhsU6pdoqqaEtXHIvAxISXm7AWLuktYLjLeQ7b/AEGg= sha512-E8I3/ST5zk/juCrmxlaiEnkc/HnjDcRvgiYD1n5vSxt7gciJW6ilOMDXEm/d6hd08uqqZm1jE/vjLcCxSdO8kA=="></script><script src="/assets/cc8521999cf151dad3fb.js" integrity="sha256-EKkP8PmyXL30d7RfRWQLrS0iozpNVGBYCrKhmYPqBH8= sha512-mUJIuWpNRp5tkLitUbAH36ZCmNTlxwbup0FYVRWcpWQDrdCydD9E2OVZ5Gf7lEUd/8e/B6K7MaWZ/9VnrkDeVg=="></script><script src="/assets/38aaa40b856262a42c9c.js" integrity="sha256-JECWxAqnVDsz67XF5KsgFrBSzH3sejTOxtsfMqc3eV0= sha512-vBC6/Ald0Du+ATLG5ipnqKjHWT4nCg4pHmvn7lmudcf0c6zF9OJUwmstT5P0iH586epsKp0LlQFidfWgDym5oQ=="></script><script src="/assets/8e17b16803a28b6f247b.js" integrity="sha256-sAM0ga2x7/nzqTo9EInvJXZfixjJ1VrpWiaZS4bAkUE= sha512-pkMJxbiQC2cBYZFdMmySbXHnZJvvY47tt9lO4gIea9PiiMKF+o5NCUg9ectFpPOIfvkUqpcNaQT2FXfYdpMBuQ=="></script>  <script nonce="MTY3LDIzLDY2LDcwLDM2LDg5LDMzLDE4MQ==" type="text/javascript">(function(){window['__CF$cv$params']={r:'719b727f5f9bab62',m:'AjH2er5wA.w.scKjMx3D7OkAHF9JyylVeL21Zh1FKaM-1654962047-0-AU3LhEB9fYI0jJ+0ykV0+FLGv4CyGmoMLQ/8ZkA860229yGbmCal7KOYM6sk6IRJFLcB3kIO5nGt+KaFL9R088CSiNLcKmOxa2YKnOEcyy+JObz004AeHZjz/qC381sCnnSa/CvT3Xf85NjRiN4UuLKxXlevm+5Tr0jcR68EueaN',s:[0x00e57e00a5,0xcdb72caeb9],}})();</script></body>
</html>
```

Since there are a bunch of JavaScript files we don't understand, let's just view it in the browser instead. A quick search using Ctrl+F to find `grey` shows us a lot of results. Let's go through them 1 by 1.

1. The first 'Grey' is the title of the server on the sidebar. It is part of the phrase 'Grey Cat The Flag'. We are unable to find much information here, there is no hidden comments in the HTML and sadly must move on.

4. The second 'Grey' is in the heading of the message container. The heading says 'Welcome to Grey Cat The Flag'. Similarly, nothing is hiding in the CSS regarding the heading.

1. The 3st 'Grey' is in a message, and the message is yellow. Looks kinda weird. It says 'grey{.....}'. This looks familiar! I have done a similar CTF before, and their flags are something like that, but it does not have grey. Not sure why it is different. This is most likely the flag, so submitting it should solve the challenge. 

5. wtf? it is wrong??? the challenge authors are literrally sooo badd they even got their own solutkion worng hahahaha.. i should open a support ticket and tell them theyu are wrong

9. they said its not the right flag and i should keep looking... i think they are just messing with me

2. wait theres another one below is says `E.g. grey{1_h4ve_read_da_rules_and_4gr33}` 

6. oh ok this one works i think the authors edited the message after i told them they were wrong.. they should give me bonus points as compensation instead.... maybe give me some kind of bug bounty,,,,

# flag

`E.g. grey{1_h4ve_read_da_rules_and_4gr33}`