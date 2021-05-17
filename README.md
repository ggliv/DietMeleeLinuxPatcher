# DietMeleeLinuxPatcher
## Linux patcher script for the Diet Melee project

## Usage
* Open your favorite file manager and drag your Melee ISO onto the icon labelled "Drag Your Melee ISO Here".
* Answer the prompt to select what version of Diet Melee you want.
* Wait for the ISO to be patched.
* Done. Open the resulting patched file in [Slippi Online](https://github.com/project-slippi/Ishiiruka/).

## Troubleshooting
To use this script you will need to have a bash interpreter and coreutils installed.

The vanilla Melee ISO used must have an md5 sum of `0e63d4223b01d9aba596259dc155a174`, otherwise xdelta will refuse to patch.

If you are running on an architecture other than amd64 (or if your distribution ), you will need to manually install the `xdelta3` package from your distro's repositories.
The bundled binary is dynamically linked and built for amd64, but this script can look for a local install of xdelta3 in your $PATH.

If you can't just drag and drop for some reason, you'll have to manually run the patcher script.
To do this, open up a terminal in the same folder as this README.
Then run `./PatchISO [PATH TO YOUR VANILLA ISO]` where [PATH TO YOUR VANILLA ISO] is... the path to your vanilla ISO.
Spaces and irregular characters will need to be escaped, use tab completion.

## Usage from git repository
This repository does not contain blobs that are usually held in the ./blob directory. If you want to run the patcher from this repository directly for some reason, you will need to replace them. I'd really recommend just using the [normally published patcher](https://diet.melee.tv/download/) though.

1. Obtain an xdelta3 binary. You can build it yourself but the normally bundled version is nabbed from the [Debian repositories](https://packages.debian.org/stable/xdelta3). The file should be placed as `./blob/xdelta/xdelta3`. Make sure it's marked executable.
2. Obtain Diet Melee xdelta diff files. Join the [Diet Melee Discord server](https://discord.gg/PwpcPtkRwU) and ask for the latest raw xdeltas.
3. Create meta-patches for each version of Diet Melee. Using xdelta, make patches for both the 64 and crystal xdeltas based off of the classic xdelta. Place the patches in `./blob/patches`. Expected names are `64diff.xdelta`, `crystaldiff.xdelta`, and `DietMeleeClassic.xdelta`.
	* i.e. `xdelta3 -e -s DietMeleeClassic.xdelta DietMeleeCrystal.xdelta crystaldiff.xdelta`
4. Run using the standard usage instructions above.