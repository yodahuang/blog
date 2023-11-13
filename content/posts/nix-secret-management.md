---
title: "Nix Secret Management"
date: 2023-11-12T17:24:44-08:00
draft: false
---

In my [previous post]({{<ref "home-intranet-with-https">}}) I mentioned that I need to store my DNS provider's credentials into my git repository, managed by Nix. How is it done in practice?

First, I use [agenex](https://github.com/ryantm/agenix), a Nix library based on [age](https://github.com/FiloSottile/age). The benefit here is that it uses your SSH key pairs as encryption key, and no GPG involved. One pain point I had with similar tool is that whenever GPG is involved, I got super confused and eventually forgot how to decrypt my files. SSH key pair, however, has quite some ways to back up (e.g. via 1Password).

Read through the tutorial, and note that the keys you put in `secrets.nix` need to include the key under `/etc/ssh/` on your target machine. The one under `/home/$USER` does not count. Really in your `secrets.nix` you need to have 2 keys. One is per system host under `/etc/ssh`, the other your personal one, normally under `~/.ssh`. See [#64](https://github.com/ryantm/agenix/issues/64) for more discussion. I have an example [here](https://github.com/yodahuang/god-complex/blob/d8343574466a95db08ebff8e1f03efab0e16bf3b/secrets/secrets.nix).

Back to my previous example. How do I read it in my Caddyfile? What the library provide is that I can do stuff like `passwordFile = config.age.secrets.secret1.path;`. But for my usecase I want the content stored inside and have stuff like `acme_dns cloudflare {env.CF_API_TOKEN}` in my Nix-generated config file. What we should not do is to call `builtins.readFile` or `lib.fileContents` to read it out. Not only is that an [insecure anti-pattern](https://github.com/ryantm/agenix#builtinsreadfile-anti-pattern), it won't work either, because `readFile` happens at "compile time", and at that time there's not even this file yet. So you need to read it at runtime. Some discussion at [here](https://github.com/divnix/digga/discussions/319). How do we do that?

Well, as our Caddy service is a systemd service under the hood (on Linux), we can generate the env file for systemd service, and then in runtime, let the caddy binary use that env.
```nix
  systemd.services.caddy = {
    serviceConfig = {
      # CF_API_TOKEN=XXX
      EnvironmentFile = config.age.secrets.cloudflare.path;
    };
  };
```
