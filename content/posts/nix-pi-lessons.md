
---
title: "Nix Pi Lessons"
date: 2023-07-30T23:06:00-07:00
draft: false
---

Following our journey on Nix, this blog covers some pitfalls and gotchas when trying to put it on a Raspberry Pi 4B.

Initial installing is pretty straight forward. Follow [official Wiki](https://nixos.wiki/wiki/NixOS_on_ARM/Raspberry_Pi) to copy the pre-built image to SD card, boot Pi, wait and you got a TTY.

## Cache

Pi is not the beefest machine for compiling stuff. Before you copy your config over or write some in place, the first thing is to set up the cache. This could save hours of compiling time. For Raspberry 4B, it's a `aarch64` device, so the cache is already included in the official one. Put something like this in `/etc/nixos/configuration.nix` (after `sudo nixos-generate-config`):
```nix
  nix = {
    settings = {
      experimental-features = "nix-command flakes";
      substituters =
        [ "https://nix-community.cachix.org" "https://cache.nixos.org/" ];
      trusted-public-keys = [
        "cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY="
        "nix-community.cachix.org-1:mB9FSh9qf2dCimDSUo8Zy7bkq5CX+/rkCWyvRCYg3Fs="
      ];
    };
  };
```

## New user

Now, you've got a user called `nixos`, without password. Worth noticing is that the current system state is not the same as the system state you got by calling `sudo nixos-generate-config` then `sudo nixos-rebuild switch`. The "current state" is a convenient one that includes editor like `vim`, has `sshd` enabled, etc. That's not the case if you rebuild from scratch.

If you have a written Nix flake config repo somewhere, it's now a good time to `scp` it over. Note that if you introduce a new user in the new config (you should), remember to call `setpasswd` to give it a password. Without it you can't even login via TTY display. If you forgot to do that, you can login as `root` and do `setpasswd $username` to give it one.

## Avoid large packages

For example, [nix-doom-emacs](https://github.com/nix-community/nix-doom-emacs) takes forever to build as it have tons of Elisp modules bundled, with native comp.

## VSCode SSH remote server

This is not exactly a Pi issue, but as Pi is normally headless, it's the perfect candidate for remote developing. So, the remote server does not work out of the box. It needs `nixos-vscode-server`. No need to hack around as suggested by [The Wiki](https://nixos.wiki/wiki/Visual_Studio_Code#Any_client_to_NixOS_host), that's probably outdated. You'll also need `"remote.SSH.useLocalServer" = false` in code config, as suggested by [This issue](https://github.com/microsoft/vscode-remote-release/issues/1721#issuecomment-597783966) if your got ssh timeout error.
