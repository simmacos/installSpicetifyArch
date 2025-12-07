# Complete Guide: Install Spotify with Flatpak and Configure Spicetify on Arch Linux

This guide will help you install Spotify via Flatpak, configure it with Spicetify to customize its interface, and block automatic updates to ensure compatibility.

---

## Prerequisites
- Arch Linux or a derivative distribution (e.g., Manjaro, EndeavourOS)
- Terminal access with `sudo` privileges
- Active internet connection

---

## 1. Install Flatpak
Flatpak is required to install Spotify from Flathub.

### Steps:
1. Update the package database:

```sh
sudo pacman -Sy
```

2. Install Flatpak:

```sh
sudo pacman -S flatpak
```

3. Add the Flathub repository:

```sh
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

4. Restart your system to complete the configuration.

---

## 2. Install Spotify Version 1.2.53
Spicetify only works with specific versions of Spotify **(Just if spicetify isn't compatible with the latest version, check on the official website)** Follow these steps to install the correct version.

### Steps:
1. Install the latest version of Spotify:

```sh
flatpak install flathub com.spotify.Client
```

2. Downgrade to version **1.2.53** using the commit hash:
- Commit hash: `117872282ffb19b9637c435164e875edb0cf3ff203186cd7f7ee47de93f70205`

```sh
flatpak update --commit=117872282ffb19b9637c435164e875edb0cf3ff203186cd7f7ee47de93f70205 com.spotify.Client
```

3. Verify the installed version:

```sh
flatpak info com.spotify.Client
```

You should see `Version: 1.2.53`.

4. Block automatic updates to prevent future incompatibilities:

```sh
sudo flatpak mask com.spotify.Client
```

---

## 3. Install Spicetify
Spicetify is a tool that lets you customize Spotify's interface.

### Steps:
1. Install Spicetify:

```sh
curl -fsSL https://raw.githubusercontent.com/spicetify/cli/main/install.sh | sh
```

2. Install the Marketplace (optional but recommended):

```sh
curl -fsSL https://raw.githubusercontent.com/spicetify/spicetify-marketplace/main/resources/install.sh | sh
```

---

## 4. Configure Spicetify
To configure Spicetify, you need to specify the correct paths for Spotify and preferences files.

### Steps:
1. Find the installation path for Spotify Flatpak:

```sh
flatpak --installations
```

It is usually located at:

```sh
/var/lib/flatpak/app/com.spotify.Client/x86_64/stable/active/files/extra/share/spotify/
```

2. Edit the Spicetify configuration file:

```sh
nano ~/.config/spicetify/config-xpui.ini
```

Set the following parameters:

```ini
spotify_path = /var/lib/flatpak/app/com.spotify.Client/x86_64/stable/active/files/extra/share/spotify/
prefs_path = /home/$USER/.var/app/com.spotify.Client/config/spotify/prefs
```

3. Grant necessary permissions to modify Spotify files:

```sh
sudo chmod a+wr /var/lib/flatpak/app/com.spotify.Client/x86_64/stable/active/files/extra/share/spotify
sudo chmod a+wr -R /var/lib/flatpak/app/com.spotify.Client/x86_64/stable/active/files/extra/share/spotify/Apps
```

4. Apply changes and start Spicetify:

```sh
spicetify backup apply
```

---

## 5. Verify Functionality
- Launch Spotify and check if Spicetify has applied the modifications.
- If necessary, reapply changes with:

```sh
spicetify apply
```

---

## 6. Customization Options
Now you can explore Spicetify's features and customize your Spotify experience! Download themes, extensions, or snippets from the integrated Marketplace.

---

## Final Notes
If you encounter issues during installation or configuration, refer to the [official Spicetify documentation](https://spicetify.app/docs) or open an issue on GitHub.

