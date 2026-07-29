# WARNING: THIS IMAGE IS IN ACTIVE DEVELOPMENT

The image corresponding to this repo is usable, but lacks some important functions. **Proceed with caution.**

## ublue-cherenkov &nbsp; [![bluebuild build badge](https://github.com/maker-gitsune/ublue-cherenkov/actions/workflows/build.yml/badge.svg)](https://github.com/maker-gitsune/ublue-cherenkov/actions/workflows/build.yml)

ublue-cherenkov is a customized Universal Blue image featuring a minimal NiriWM/Waybar-based desktop. It is based off of the uBlue base-main image with additions to get most of the way to a “complete” tiling WM setup not including things such as user-specific apps, brand-specific printer support and the like.

It exists because layering/swapping that many packages on the uBlue Sericea image would make updating longer/more complex (also because that specific image [is no longer a thing](https://github.com/ublue-os/main/issues/927) so it could not have been used as a base either). The main use-case (out-of-box) is a single-user general purpose OS for a laptop/desktop.

### Notable packages/features (check [recipe.yml](./recipes/recipe.yml) for more information):
 - Desktop/interface:
   - NiriWM
   - Waybar
   - Fuzzel
   - SwayNC
 - display manager via greetd+tuigreet
 - foot (intended as a fallback)
 - supporting things:
   - gammastep
   - brightnessctl
   - swaybg
   - swaylock
   - swayidle
   - kanshi
   - wl-mirror
 - audio via pipewire
 - file manager - Thunar (Yazi is also currently included)
 
 ### Default apps (via Flatpak):
 - Browser (Zen)
 - Flatpak management:
   - Flatseal
   - Warehouse
   - Bazaar
 - Terminal emulator (Ptyxis)
 - System monitor (MissionCenter)
 - Video player (Mpv)
 - Office suite (onlyoffice)
 - Photo viewer (pineapple-pictures)
 - Camera (Snapshot)
 - light photo annotation/editing (Gradia)
 - Calculator (GNOME calculator)
 - Clock (GNOME clocks)
 ## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/maker-gitsune/ublue-cherenkov:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/maker-gitsune/ublue-cherenkov:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## todo
- [ ] include default/baseline config. files
- [ ] opiniated "second stage install"
  -  system theming and associated configuration files
  -  menus/utilities
- image variants?
  -  [ ] virtualisation support
  -  [ ] Nvidia-specific?

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/maker-gitsune/ublue-cherenkov
```
