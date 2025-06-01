# Intro

Parsec is a remote desktop tool like teamviewer, but does not allow custom resolutions by default, so the user has to stick to the default ones. 
Example: laptop has a 16:10 ratio with 3840x2400 pixels, which is not listed. Creating a custom resolution would enable using the full screen.
This is my personal guide and assumes only one client, e.g. a laptop is used to connect to the host machine.

# Setup

## Create a custom resolution (On Host PC)

### Option 1: 

Pick one of the resolutions in this repo and run the .reg file

### Option 2:

Create a custom resolution, that is not listed anywhere:

- Open `regedit.exe` and navigate to (or create) `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Parsec\vdd`
- Create a new key, that contains only a number, e.g. `0`, if it already exists pick the next available number, avoid duplicates
- Create the following `DWORD (32-Bit)` values:
  - Name: `height`, Value: height in pixels with decimal base
  - Name: `width`, Value: width in pixels with decimal base
  - Name: `hz`, Value: screen refresh rate (Hertz) with decimal base

## Set custom resolution (On Client PC)

- Decide on one custom resolution created, that should always be used
- Open either of these two, depending on which exists
  - `C:\ProgramData\Parsec\config.json`
  - `C:\Users\%USERPROFILE%\AppData\Roaming\Parsec`
- set `server_resolution_x` to the width in pixels of the resolution decided on
- Set `server_resolution_y` to the respective height
- set `encoder_fps` to the respective refresh rate
- Make sure the custom res is used, by using `Use Client Resolution`

## Persist custom resolution

After a reconnect to the host, the resolution will automatically revert so something standard by parsec. To persist the custom resolution, the file needs to be set `read-only`, to prevent parsec from modifying it.

- Ensure custom resolution data is set in `config.json`
- Make the file `Read-only`

# Bonus

## Audio workaround

If the host machine has a headset, headphones or whatever conencted, the audio will be forwarded to the client.  
If the host has no audio device attached though, the client will hear nothing, even if host's volume is 100%.

To fix this, either headphones can be plugged in on the host, or a dummy headphone can be built like this:
- Get an aux port that can be soldered
- Conenct Left with GND using a 100 Ohm resistor
- Connect Right with GND using a 100 Ohm resistor
- Plug the dummy headphone into the host machine
- Check if the host shows a notification like "Headphones plugged in"
