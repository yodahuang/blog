---
title: "Home Intranet With Https"
date: 2023-10-27T23:46:00-07:00
draft: false
---

It took me quite a while to understand how to do the whole thing. So I'd share it here.

## The problem

I've go quite some services scattering in my local network. That OctoPrint instance is at `192.168.xx.yy:1234`, that TP-Link ethernet switch has a web UI at `192.168.ww.zz:5678`. It's impossible to remebber these IP:ports. So we need some easier to remember aliases. A bookmark system to list them all is a bonus.

## Why not?

- A bookmark manager that have all of them: I like to overengineer things. It's also easier to share the page with household members.

## The end result

All the service got two urls: `https://foo.int.yanda.rocks` and `http://foo.home`.
![Current state of my.home](./my_home_demo.png)

## Implementation

### DNS

DNS is the system that maps your normal looking address (http://foo.bar) to an IP address (e.g. 192.168.0.1). That's why it's called Domain Name System. For our purpose, we can either use a private DNS server (that serves http://foo.home, only when you opt in on your device to use your local DNS server), or use the public one (that redirect a domains you control to the services you serve). My suggestion is go straight to the public DNS route.

#### Public DNS

Get your own domain name, then give route a wildcard subdomain to your local ip. In the following example, I'm routing all *.int.yanda.rocks to 192.168.4.117, where that address is where I set up my [reverse proxy]({{< ref "#reverse-proxy">}}). Note that I simply link a domain name to a port. It can only be 80 or 443. Our services may be on different port though, and that's why we need that reverse proxy.

![Cloudflare DNS panel](./cloudflare_dns.png)

#### Private DNS

You can run your own DNS server. For example, with dnsmasq, you may have a config file that have the following content, which route all `.home` query to your specific address
```
address=/.home/192.168.4.117
```
or with AdGuard Home, where it has a "DNS rewrite" option.

### Reverse proxy

We hinted reverse proxy previously. That's a program running on one of your local controlled machines that takes in client request, and then dispatch them to the "real machine". For example, It may get a request from a browser to visit `nas.int.yanda.rocks`. It has the knowledge that the NAS is actually at `http://foo.bar:4200`, so it would "reroute" the request there. The client does not need to know the actual address of the NAS. It always ask the reverse proxy first.

I've only use Caddy (some other choices includes Nginx and Traefik). There's [the official doc](https://caddyserver.com/docs/quick-starts/reverse-proxy), and it's super easy. The tricky part is tot get https working.

### HTTPS

To use https, you need to show to the world "The one who's serving contents at the domain also is the controller of the domain", to avoid man-in-the-middle attack. There's several ways to do that. See [all the challenge types](https://letsencrypt.org/docs/challenge-types/). For our purpose, the best one is the DNS-01 challenge, instead of the commonly used HTTP-01 challenge. Let's Encrypt suppoort only that for wildcard domain names, and it does not require exposing ports in your internal network to the public one.

With Caddy, it's again not hard to do that. With Caddy in Nix though, that's a problem as the dns functionality is included in the form of a plugin. The Caddy package in Nix, as of Nov 2023, does not support that. Luckily we have a unmerged pr: [#259275](https://github.com/NixOS/nixpkgs/pull/259275). For how to use it, you can refer to my configuration: [pacakge](https://github.com/yodahuang/god-complex/blob/d8343574466a95db08ebff8e1f03efab0e16bf3b/pkgs/meowdy.nix) and [usage](https://github.com/yodahuang/god-complex/blob/d8343574466a95db08ebff8e1f03efab0e16bf3b/hosts/earl_grey/caddy.nix).

If you wonder how do I store the API secret in a Git repository in my Nix setup, see [my other post]({{<ref "posts/nix-secret-management" >}}).

### Dashboard

You'll be surprised about how many projects are about dashboard. A recent favorite of the community is [homepage](https://github.com/gethomepage/homepage), but I'm still using [Homer](https://github.com/bastienwirtz/homer), which just works, is simple and works nicely with Nix. I have my Homer package definition [here](https://github.com/yodahuang/god-complex/blob/d8343574466a95db08ebff8e1f03efab0e16bf3b/pkgs/homer.nix).