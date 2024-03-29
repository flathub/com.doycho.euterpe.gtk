# Euterpe GTK

This builds the [GTK Client](https://github.com/ironsmile/euterpe-gtk/) for [Euterpe](https://listen-to-euterpe.eu/).

## Gstreamer

Gstreamer is not explicitly listed as dependency and is expected to be present.

## Updateing Dependencies

First make sure to clone and checkout the appropirate version of
[python-crypthography](https://github.com/pyca/cryptography).

The [flatpak-cargo-generator](https://github.com/flatpak/flatpak-builder-tools/tree/master/cargo) and
[flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools/tree/master/pip) are used
in order to generate the `pypi-dependencies.json` and `cargo-sources.json`.

```sh
flatpak-cargo-generator ../cryptography/src/rust/Cargo.lock -o cargo-sources.json
flatpak-pip-generator --requirements requirements.txt --output pypi-dependencies
```

where  `../cryptography/src/rust/Cargo.lock` is from the previusly checked out
crypthography repo and version. Make sure that the checked out version is in sync with
the one in `pypi-dependencies.json`.

Then copy the sources for `cryptography`, `cffi` and `pycparser` from `pypi-dependencies.json`
into `cryptography.json`.

Sometimes the build tools (such as `setuptools_rust`) may have to be updated in
`python-setuptools-rust.json`. I have no idea how to do that correctly so I am generally
copying what [Thonny](https://github.com/flathub/org.thonny.Thonny) did last.

Pray 🙏

## Building Locally

To build the flatpak the same way it is built on the Flathub build servers run:

```sh
flatpak run org.flatpak.Builder -v --bundle-sources --install-deps-from=flathub --user \
    --force-clean build-dir com.doycho.euterpe.gtk.json
```
