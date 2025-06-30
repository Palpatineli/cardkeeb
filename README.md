# Slimkeeb 36 Firmware

This is the zmk firmware for [Slimkeeb36](https://github.com/Palpatineli/slimkeeb36)

## Howto

Fork this repo, then make a copy of the `config/gallium36.keymap` file. Rename it to anything, for example `my_map.keymap`.
Modify the `build.yaml` file and change the values of the `-DKEYMAP_FILE` to point to your new file.
In the above example that line would be `cmake-args: -DKEYMAP_FILE=../../config/my_map.keymap`.
Then follow the [official guide](https://zmk.dev/docs/keymaps) to make your own keymap.

After you are done. Add the new file, commit and push.
An action will run to compile the firmware.
Go into `Actions` on your github fork's page to check if the new run finishes (usually takes a few minutes).
If there's an error, click into the workflow to see the error message and debug.
Otherwise download the artifact.

Unzip the file and you'll find 3 files in the folder: reset, left and right.
Connect one half of the board via USB to your computer.
Use a toothpick through the hole above the board to double-press the reset bottom.
You'll hear a sound and a new drive will appear.
Drag the `.utf2` file onto that drive, left file for the left half and right file for the right half.
Once the copy is done the drive will automatically disappear.
Connect the new bluetooth device.

### When to use the reset file
Bluetooth signature will persist through firmware flashing, unless you flash it with the reset file first.
Flashing with the reset file then the actual firmware file will fix:
1. Change which half is master and which is slave.
2. You removed the bluetooth device from windows and adding it back causes an error.
3. Other mysterious bluetooth connection failures. You should try reset before looking for other fixes.

### Limitations to keymapping
Due to the special design of the key matrix there is a major limitation wrt keymapping.
You can't have combo's between keys of the same column.
The following pairs will not work in a combo. They do not trigger a phantom press but will not trigger a combo either:
- <2> <3>
- <6> <7>
- <21> <22>
- <27> <28>
