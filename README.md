# Euterpe GTK

This builds the [GTK Client](https://github.com/ironsmile/euterpe-gtk/) for [Euterpe](https://listen-to-euterpe.eu/).

## Gstreamer and libhandy

Gstreamer and libhandy are not explicitly listed as dependencies and are expected to be present.

## Manual Install and Run

Make sure you follow the [setup guide for your Linux distribution](https://flathub.org/en/setup) before installing.

```bash
flatpak install flathub com.doycho.euterpe.gtk
flatpak run com.doycho.euterpe.gtk
```

## Building

```bash
git clone git@github.com:flathub/com.doycho.euterpe.gtk.git
flatpak run org.flatpak.Builder build-dir --user --ccache --force-clean --install com.doycho.euterpe.gtk.yaml
```

## Updating Python Modules

```bash
flatpak-pip-generator --runtime=org.gnome.Sdk//50 --yaml --checker-data --requirements-file=requirements.txt --prefer-wheels=keyring,cryptography
```
