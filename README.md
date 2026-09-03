# nsxiv

My customized build of [nsxiv](https://github.com/nsxiv/nsxiv).

This build is used by my Arch Linux and Debian dwm setup.

`nsxiv` is compiled from source from this repository by `dwm-install`; it is not installed from the Arch Linux or Debian repositories.

## Installation

Clone the repository:

```sh
git clone https://github.com/rabbi-lion/nsxiv.git
cd nsxiv
```

Build and install:

```sh
make
sudo make install-all
```

On a fresh system, the recommended method is to use my post-install script:

```text
https://github.com/rabbi-lion/dwm-install
```

## Usage

`nsxiv` is used as the default image viewer in my dwm environment.

The surrounding setup provides:

- directory-aware image opening
- Thunar integration
- Trash support
- common image MIME associations
- keyboard handling
- a user-local desktop entry

The helper scripts and desktop entry are provided by my dotfiles repository:

```text
https://github.com/rabbi-lion/dotfiles
```

## Thunar integration

Images opened from Thunar use:

```text
~/.local/bin/nsxiv-rifle
```

This helper opens the selected image together with the other supported images in the same directory.

The user-local desktop entry is:

```text
~/.local/share/applications/nsxiv.desktop
```

## Trash support

The nsxiv key handler is:

```text
~/.config/nsxiv/exec/key-handler
```

It allows images to be moved to Trash from nsxiv.

## Image associations

`dwm-install` configures nsxiv as the default viewer for common image formats, including:

```text
JPEG
PNG
GIF
WebP
BMP
TIFF
SVG
AVIF
HEIF
HEIC
JPEG XL
JPEG 2000
```

PostScript is intentionally not assigned to nsxiv so document associations such as Zathura remain intact.

## Scaling

Stock nsxiv scaling behavior is preserved.

No forced `SCALE_FIT` source modification is used, and the file-manager helper does not force `-s f`.

## Configuration

nsxiv configuration is maintained in this repository.

After making source changes, rebuild and reinstall:

```sh
sudo make clean install
```

## Related repositories

```text
https://github.com/rabbi-lion/dwm-install
https://github.com/rabbi-lion/dotfiles
https://github.com/rabbi-lion/dwm
https://github.com/rabbi-lion/st
https://github.com/rabbi-lion/dwmblocks
```

## License

This repository retains the original nsxiv GNU General Public License.

See `LICENSE` for the full license text.
