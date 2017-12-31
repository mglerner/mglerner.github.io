<!--
.. title: Chromebooks for the kids
.. slug: chromebooks-for-the-kids
.. date: 2017-12-31 17:58:37 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

# Chromebook for the kids

My oldest daughter is 9, and the twins are 6, so it's probably time to get them involved in computer things. I could have done this earlier, but I definitely screwed up with the kids by introducing tech/books/etc. before they were ready, so I decided to wait. The kids are definitely ready, so here are the goals:

* Programming
    * Minecraft seems to be the best for this, but I want more than 2GB of RAM. Preferably 8GB.
    * [Scratch](https://scratch.mit.edu) also seems to get a ton of great recs.
* Access to the internet
* Having an office suite around. The 9yo will be writing papers at school next year, etc.

My original thought was that I'd get a cheap desktop: either a Windows box or a refurbished Mac. I was leaning against Linux because I'm old and it seems like there's a big barrier to entry for Linux. I want this to just work for the kids. Then someone pointed out that we'll be traveling out of the country next year, so a desktop is a bad idea. The cheapo version of a laptop is a Chromebook, but I wanted one capable of running Minecraft. I find a really nice [guide to setting up Minecraft on a Chromebook](https://platypusplatypus.com/chromebooks/play-minecraft-chromebook/). Of all things, the answer is to install Linux via [crouton](https://github.com/dnschneid/crouton). Who knew. So, I'll give that a try. The site also has a nice guide to Minecraft-capable Chromebooks. On the high end, the Pixel has all of the stats I could want ... but $1k seems like quite a bit to spend on a "cheapo" laptop. There were some nice $200 models, but I settled on the Asus Flip 2 (Intel Core m3, 4GB of RAM ... not quite the 8GB I wanted). I think the kids will really like the touchscreen and flipscreen. Hopefully they won't fight too much over the single computer.

So, as per the [guide](https://platypusplatypus.com/chromebooks/play-minecraft-chromebook/),

* Be prepared to [Powerwash](https://platypusplatypus.com/chromebooks/powerwash-chromebook-full-recovery/)/revert to factory settings. (In fact, I had to do this because apparently I screwed up a root password in the next step.)
* Enable [Developer Mode](https://platypusplatypus.com/chromebooks/enable-developer-mode-chromebook/).
* Install [crouton](https://github.com/dnschneid/crouton) and the crouton Chrome extension (link on crouton page).
* Install Linux
    * "Ctrl + Alt + T" gives you a command terminal in Chrome
    * `shell` gives you a shell
    * `sudo sh -e ~/Downloads/crouton -t touch,kde-desktop`

* Switch back to the Chromebook side (shift+ctrl+alt+left arrow at the top of the keyboard).
* Download the Linux Java version of Minecraft from minecraft.net
* Switch back to the linux side (shift+ctrl+alt+right arrow at the top of the keyboard).
* Put Minecraft in a stable place
    * `mkdir ~/Games`
    * `mv ~/Downloads/Minecraft.jar ~/Games`
* You can launch via the command line: `java -jar ~/Games/Minecraft.jar`
* You can make a KDE shortcut to launch it. It's very particular.
    * Open up `kmenuedit` and make a new item under Games.
    * Call it Minecraft.
    * Make the command `java -jar ./Minecraft.jar`
    * Under Advanced, make the Work path `~/Games` and select `Run in terminal`
* You can also go into `~/Games`, open it up in the file browser via `xdg-open .` then drag the Minecraft jar file onto the desktop. That gives you an icon which, when double-clicked, will launch Minecraft.

Be aware that exiting developer mode will erase all of the Linux setup from above. Reinstalling it takes about 5 minutes of typing and 45 minutes of letting the computer churn.

So far, the kids seem more than happy with this setup. The crouton Linux install seems to be shared no matter who logs in on the Chromebook, so they can all log in individually on the ChromeOS side, but share the same Linux side. They don't seem to have a problem opening up a command terminal and sudo-launching kde, which is either cool or disturbing. Not sure which :).
