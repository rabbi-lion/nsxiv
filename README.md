# nsxiv

My customized build of [nsxiv](https://github.com/rabbi-lion/nsxiv).

Used by my Arch Linux and Debian dwm setup. `nsxiv` is compiled from
source from this repository by `dwm-install`; it is not installed
from the Arch Linux or Debian repositories.

## Installation

```sh
git clone https://github.com/rabbi-lion/nsxiv.git
cd nsxiv
make
sudo make install-all
```

On a fresh system, use my post-install script instead:

```
https://github.com/rabbi-lion/dwm-install
```

## Thunar / GVfs integration

If you use Thunar or GVfs and want the same image-opening behavior
as my dwm setup, install the nsxiv integration files from my
dotfiles repository.

Clone the dotfiles temporarily:

```sh
git clone --depth=1 https://github.com/rabbi-lion/dotfiles.git /tmp/dotfiles
```

Create the required directories:

```sh
mkdir -p ~/.local/bin ~/.local/share/applications ~/.config/nsxiv/exec
```

Install the helper, desktop entry, and key handler:

```sh
cp /tmp/dotfiles/.local/bin/nsxiv-rifle ~/.local/bin/
cp /tmp/dotfiles/.local/share/applications/nsxiv.desktop ~/.local/share/applications/
cp /tmp/dotfiles/.config/nsxiv/exec/key-handler ~/.config/nsxiv/exec/
```

Make the helper scripts executable:

```sh
chmod +x ~/.local/bin/nsxiv-rifle ~/.config/nsxiv/exec/key-handler
```

Point the desktop entry at the absolute path of `nsxiv-rifle`:

```sh
sed -i "s|^Exec=.*|Exec=$HOME/.local/bin/nsxiv-rifle %f|" \
    ~/.local/share/applications/nsxiv.desktop
```

This avoids depending on `~/.local/bin` being present in `PATH`.

Register nsxiv as the default viewer for common image formats:

```sh
for type in \
    image/bmp \
    image/gif \
    image/jpeg \
    image/jpg \
    image/png \
    image/tiff \
    image/x-bmp \
    image/x-portable-anymap \
    image/x-portable-bitmap \
    image/x-portable-graymap \
    image/x-tga \
    image/x-xpixmap \
    image/webp \
    image/heic \
    image/svg+xml \
    image/jp2 \
    image/jxl \
    image/avif \
    image/heif
do
    xdg-mime default nsxiv.desktop "$type"
done
```

PostScript is intentionally not assigned to nsxiv, so document
associations such as Zathura remain intact.

Verify the association:

```sh
xdg-mime query default image/jpeg
```

It should return:

```
nsxiv.desktop
```

Remove the temporary clone:

```sh
rm -rf /tmp/dotfiles
```

## Usage

In my dwm environment, the surrounding setup provides:

- directory-aware image opening
- Thunar integration
- Trash support
- common image MIME associations
- keyboard handling
- a user-local desktop entry

The helper scripts and desktop entry come from my dotfiles
repository:

```
https://github.com/rabbi-lion/dotfiles
```

### Thunar

Images opened from Thunar use:

```
~/.local/bin/nsxiv-rifle
```

This opens the selected image together with the other supported
images in the same directory.

The user-local desktop entry is:

```
~/.local/share/applications/nsxiv.desktop
```

### Trash support

The nsxiv key handler is:

```
~/.config/nsxiv/exec/key-handler
```

It moves images to Trash from within nsxiv. GVfs is required for
this to work.

## Scaling

Stock nsxiv scaling behavior is preserved.

No forced `SCALE_FIT` source modification is used, and the
file-manager helper does not force `-s f`.

## Configuration

nsxiv configuration is maintained in this repository. After making
source changes, rebuild and reinstall:

```sh
sudo make clean install
```

## Related repositories

```
https://github.com/rabbi-lion/dwm-install
https://github.com/rabbi-lion/dotfiles
https://github.com/rabbi-lion/dwm
https://github.com/rabbi-lion/st
https://github.com/rabbi-lion/dwmblocks
```

## License

This repository retains the original nsxiv GNU General Public
License. See `LICENSE` for the full license text.
