# Ubuntu (25.04) Gnome, Tweaks-tool and system-wide configurations backup

* Extensions are stored in ```~/.local/share/gnome-shell/extensions```.

# Restore
- Install **Extension Manager** with `flatpak install flathub com.mattjakeman.ExtensionManager`.
- Install the extensions listed in `gnome_extensions_list.txt`.
- Run `dconf load /org/gnome/shell/extensions/ < gnome-shell-extensions-backup.dconf` to set the extensions configurations. 
- Restart the session/system to see the effects.
- (optional) Restore all Gnome-wide settings, including **Gnome-tweaks** configurations using `dconf load -f / < complete_gnome_saved_settings.dconf`.
- Additionally, you can backup and restore all the GNOME settings and other configurations using `flatpak install flathub io.github.vikdevelop.SaveDesktop` flatpak app.

# Backup
- To backup only gnome-shell extentions, run `dconf dump /org/gnome/shell/extensions/ > gnome-shell-extensions-backup.dconf` and for all system-wide configurations, run `dconf dump / > complete_gnome_saved_settings.dconf`.

# Chromium browsers config

- Enable flags in `chrome://flags`, `brave://flags` and `edge://flags`.
- Copy browser files from `/usr/share/applications/` to `~/.local/share/applications/`.
- For each of the copied files, jump to the line that begins with `Exec=` and ends with `%U` and append as shown below. Append the same to the line that begins with `Exec=` and ends with `--inprivate` or `--incognito`.
- Alternatively, create `chrome-flags.conf`, `brave-flags.conf`, `edge-flags.conf` files in `~/.config` and add the flags to the ***-flags.conf** files.
- Restart the system or session.

| Browser | copy *.desktop file | `*://flags` |
|:---|---|---:|
| Google Chrome | `sudo cp /usr/share/applications/google-chrome.desktop ~/.local/share/applications/` | `#fluent-overlay-scrollbars` `#fluent-scrollbars` `#ozone-platform-hint` `#wayland-ui-scaling` `#root-scrollbar-follows-browser-theme` `#link-preview` |
| Brave | `sudo cp /usr/share/applications/brave-browser.desktop ~/.local/share/applications/` | `#fluent-overlay-scrollbars` `#fluent-scrollbars` `#ozone-platform-hint` `#wayland-ui-scaling` `#root-scrollbar-follows-browser-theme` `#linork-preview` `#middle-button-autoscroll` |
| Microsoft Edge | `sudo cp /usr/share/applications/microsoft-edge.desktop ~/.local/share/applications/` | Only enable flags in the `.desktop` file |

| Browser | Code to append |
|:---|---:|
| Google Chrome | `--enable-features=MiddleClickAutoscroll,TouchpadOverscrollHistoryNavigation --disable-features=GlobalShortcutsPortal` |
| Brave Browser | `--enable-features=TouchpadOverscrollHistoryNavigation --disable-features=GlobalShortcutsPortal` |
| Microsoft Edge | `--enable-features=MiddleClickAutoscroll,TouchpadOverscrollHistoryNavigation,UseOzonePlatform,WaylandWindowDecorations --ozone-platform=wayland --disable-features=GlobalShortcutsPortal` |

For GRUB configuration, install the GRUB theme but comment out the `GRUB_BACKGROUND` flag to avoid any graphical glitches.

