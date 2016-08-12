---
layout: post
title:  "Swimming in the Digital Ocean"
date:   2016-08-12 12:24:07 -0400
---


So I've spent the better part of three days experimenting with Digital Ocean droplets and working with Google Domains to get a personal portfolio setup. The idea was I would be able to host my portfolio and several projects that can be used as examples of my work to perspective employers or really anyone who wanted to check them out. Simple idea, sounded pretty easy to do however it took me a while to get everything straightened out.


**Digital Ocean**

So for anyone who doesn't know what Digital Ocean is you should check them out! I'll post a referral link that will give you $10 worth of credit there which can give you 2 months of access to one of their droplets.

[Digital Ocean Referral Link](https://m.do.co/c/741062b30995)

Digital Ocean is a cloud computing platform, or simply it's a server hosted in the cloud for you to use. You can create a droplet (server) with a variety of options available from different operating systems to one-click-apps that pre-install the software you might need to get it up and running quickly. The whole process of creating my droplet and getting access to it took about 5 minutes, super fast and easy! I ended up choosing the cheapest droplet option they have since I didn’t think I would need much in the way of computing power or space for a little portfolio and $5/mo really wasn’t a bad deal for a fully functioning server with reliable uptime.

I’m going to create another post with the setup instructions and commands I used to get my droplet up and running from scratch, this isn’t really a how-to type of post, more of a log of my adventures.

So this little adventure began with me setting up and tearing down my little droplet’s over and over again until I finally got smart. Here is my first little tidbit of wisdom for you, **when you first create a droplet, power it down and take a snapshot before doing ANYTHING**.  Snapshots are basically backups of your machine as it is at that moment. It helps you restore back to a working setup if you add something and it doesn’t go according to plan, or if an update breaks your app. All you do is power off your server and select the snapshot you want to restore from and it takes care of it for you. Next time you log back in your settings will be restored and you can either try again or remember not to touch whatever it was that broke everything.

My first snapshot was called ‘initial setup’ and it was an easy way to restore my droplet back to it’s original settings when it was first created. After destroying and recreating my droplet over and over I decided this was the smart thing to do. Second little piece of advice, **every time you make any big changes make sure to make another snapshot**. Adding a bunch of firewall rules? Snapshot before so you can go back. Changing php versions … snapshot. It’s only going to make things easier when something goes wrong. I ended up only keeping 2 snapshots of my droplet once everything was setup the way I liked it. I have my initial setup just incase I want to completely wipe my droplet and I have one that has LEMP, Rails and several other programs installed for my production environment. It also has all of my security settings and SSH keys saved.


**Profile Page**

With all of that done it was time for me to throw up a quick coming soon page and call it good for now. A little bootstrap here, some fonts and custom styling there and I have something that’s at least presentable for now. I know I’m going to be changing it eventually, but I just wanted something out there for now. You can view it at [http://www.breynolds.co](http://www.breynolds.co). I’m really enjoying playing with my droplet and I might invest in a second one that I can use to test different setups and configurations on before setting it live to my production server. Like a real developer!
