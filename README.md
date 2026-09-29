# Euterpe GTK

This builds the [GTK Client](https://github.com/ironsmile/euterpe-gtk/) for
[Euterpe](https://listen-to-euterpe.eu/).

## Implicit Dependencies

Gstreamer and LibHandy are not explicitly listed as dependencies and are expected to be
present.

## Updating The Runtime

Get the current stable version of the Gnome runtime from its
[release calendar](https://release.gnome.org/calendar/). Note that runtime releases are
synchronized with Gnome version releases.

## Updating Dependencies

The [flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools/tree/master/pip)
is used in order to generate the `pypi-dependencies.json`.

```bash
flatpak-pip-generator --requirements requirements.txt \
    --runtime=org.gnome.Sdk//50 \
    --output pypi-dependencies \
    --prefer-wheels=keyring,cryptography
```

Make sure the runtime used in the `flatpak-pip-generator` command is the same one used by
the application in `com.doycho.euterpe.gtk.json`.

## Building Locally

To build the flatpak the same way it is built on the Flathub build servers run:

```sh
flatpak run org.flatpak.Builder -v --bundle-sources --install-deps-from=flathub --user \
    --force-clean build-dir com.doycho.euterpe.gtk.json
```
