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

### Thunar / GVfs integration

If you use Thunar or GVfs and want the same image-opening behavior as my dwm setup, install the nsxiv integration files from my dotfiles repository.

Clone the dotfiles repository:

```sh
git clone --depth=1 https://github.com/rabbi-lion/dotfiles.git /tmp/dotfiles
```

Create the required directories:

```sh
mkdir -p ~/.local/bin ~/.local/share/applications ~/.config/nsxiv/exec
```

Install the nsxiv helper, desktop entry, and key handler:

```sh
cp /tmp/dotfiles/.local/bin/nsxiv-rifle ~/.local/bin/
cp /tmp/dotfiles/.local/share/applications/nsxiv.desktop ~/.local/share/applications/
cp /tmp/dotfiles/.config/nsxiv/exec/key-handler ~/.config/nsxiv/exec/
```

Make the helper scripts executable:

```sh
chmod +x ~/.local/bin/nsxiv-rifle ~/.config/nsxiv/exec/key-handler
```

Configure the desktop entry to use the absolute path to `nsxiv-rifle`:

```sh
sed -i "s|^Exec=.*|Exec=$HOME/.local/bin/nsxiv-rifle %f|" ~/.local/share/applications/nsxiv.desktop
```

Configure nsxiv as the default viewer for supported image formats:

```sh
for type in image/bmp image/gif image/jpeg image/jpg image/png image/tiff image/x-bmp image/x-portable-anymap image/x-portable-bitmap image/x-portable-graymap image/x-tga image/x-xpixmap image/webp image/heic image/svg+xml image/jp2 image/jxl image/avif image/heif; do xdg-mime default nsxiv.desktop "$type"; done
```

Remove the temporary dotfiles clone:

```sh
rm -rf /tmp/dotfiles
```

You can verify the default image association with:

```sh
xdg-mime query default image/jpeg
```

It should return:

```text
nsxiv.desktop
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

The desktop entry is configured to launch `nsxiv-rifle` using its absolute path so graphical applications do not depend on `~/.local/bin` being present in `PATH`.

## Trash support

The nsxiv key handler is:

```text
~/.config/nsxiv/exec/key-handler
```

It allows images to be moved to Trash from nsxiv.

GVfs is required for the Trash functionality used by this setup.

## Image associations

The Thunar / GVfs integration configures nsxiv as the default viewer for common image formats, including:

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

The corresponding MIME associations are:

```text
image/bmp
image/gif
image/jpeg
image/jpg
image/png
image/tiff
image/x-bmp
image/x-portable-anymap
image/x-portable-bitmap
image/x-portable-graymap
image/x-tga
image/x-xpixmap
image/webp
image/heic
image/svg+xml
image/jp2
image/jxl
image/avif
image/heif
```

These associations allow file managers such as Thunar to open supported images through `nsxiv.desktop`.

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
