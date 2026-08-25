# ublue-cherenkov &nbsp; [![bluebuild build badge](https://github.com/maker-gitsune/ublue-cherenkov/actions/workflows/build.yml/badge.svg)](https://github.com/maker-gitsune/ublue-cherenkov/actions/workflows/build.yml)
> [!WARNING]  
> This image is in active development; it is usable, but potentially breaking changes might still occur. **Proceed with caution.**

ublue-cherenkov is a customized Universal Blue image featuring a minimal NiriWM/Waybar-based desktop. It is based off of the uBlue base-main image with additions and some baseline configuration files to get most of the way to a “complete” tiling WM setup not including things such as user-specific apps, brand-specific printer support and the like.

It exists because layering/swapping that many packages on the uBlue Sericea image would make updating longer/more complex (also because that specific image [is no longer a thing](https://github.com/ublue-os/main/issues/927) so it could not have been used as a base either). The main use-case (out-of-box) is a single-user general purpose OS for a laptop/desktop.

### Notable packages/features (check [recipe.yml](./recipes/recipe.yml) for more information):
 - Desktop/interface:
   - NiriWM
   - Waybar
   - Fuzzel
   - SwayNC
 - greetd+tuigreet for the display manager
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
 - iwd as WiFI backend
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
 - Photo viewer (eye of GNOME)
 - Camera (Snapshot)
 - light photo annotation/editing (Gradia)
 - Calculator (GNOME calculator)
 - Clock (GNOME clocks)
 ## [Baseline Configuration files](files/system/etc)
 ublue-cherenkov ships with some baseline configuration files for Niri, Waybar, Fuzzel and greetd. All of those configuration files have been modified from their defaults mostly to achieve minimum viable function/integration with the included packages ([example photos](pictures/)):
  - Niri - the default config.kdl has been modified to start SwayNC/SwayOSD/xfce-polkit etc. and has keybinds for cliphist and SwayOSD along with some minor styling.
  - waybar - the default SwayWM workspace/window modules have been replaced with their Niri equivalents, font set to use the installed JetBrains Mono Nerd font and to have a module for SwayNC. It also has some minor styling and a minimal module selection including a custom module for wlogout.
  - greetd - the included configuration file offers a baseline setup for tuigreet and should ensure proper system function without user intervention (manual configuration is normally needed to set it up).
  - fuzzel - modifications to somewhat match minor styling in Niri/waybar configurations, use JetBrains Mono Nerd Font and enable per-app actions.
  - foot - use JetBrains Mono Nerd Font.
  - swaync - some minor styling to match the others.
  - a config file to enable networkmanager to use iwd.
  - an xdg-desktop-portals config that should allow for expected/normal file chooser behavior OOTB.
 ## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  - The image comes with its own selection of Flatpaks, so a ```flatpak uninstall --all``` is recommended if you are rebasing a brand-new install to specifically use ublue-cherenkov.
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

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/maker-gitsune/ublue-cherenkov
```
## todo:
- [x] include default/baseline config. files
  - Niri, waybar, fuzzel configurations added in release 26.08
  - Foot, swaync configuration added in release 26.08.1
- [ ] opiniated "second stage install"
  -  system theming and associated configuration files
  -  menus/utilities
- image variants?
  -  [ ] virtualisation support
  -  [ ] Nvidia-specific? 