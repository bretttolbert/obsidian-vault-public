# gsettings

## Configure GNOME desktop settings


###### Turn off the goddamned bell/bark/ding/splash sound in gnome easy-tag

It is inaccessible through the GUI now WTF.

```bash
gsettings set org.gnome.desktop.sound event-sounds false
```

To make it permanent:

```bash
echo "gsettings set org.gnome.desktop.sound event-sounds false" >> ~/.bashrc
```
