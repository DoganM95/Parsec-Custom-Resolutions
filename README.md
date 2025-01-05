# Intro

Parsec is a remote desktop tool like teamviewer, but does not allow custom resolutions by default, so the user has to stick to the default ones. 
Example: laptop has a 19:10 ratio with 3840x2400 pixels, which is not listed. Creating a custom resolution would enable using the full screen.
This is my personal guide and assumes only one client, e.g. a laptop is used to connect to the host machine.

# Setup

## Create a custom resolution

- Open `regedit.exe` and navigate to (or create) `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Parsec\vdd`
- Create a new key, that contains only a number, e.g. `0`, if it already exists pick the next available number, avoid duplicates
- Create the following `DWORD (32-Bit)` values:
  - Name: `height`, Value: height in pixels with decimal base
  - Name: `width`, Value: width in pixels with decimal base
  - Name: `hz`, Value: screen refresh rate (Hertz) with decimal base

## Set custom resolution

- Decide on one custom resolution created, that should always be used
- `C:\ProgramData` is a hidden folder, google how to show it
- Open `C:\ProgramData\Parsec\config.json`
- set `server_resolution_x` to the width in pixels of the resolution decided on
- Set `server_resolution_y` to the respective height
- set `encoder_fps` to the respective refresh rate

## Persist custom resolution

After a reconnect to the host, the resolution will automatically revert so something standard by parsec. To persist the custom resolution, the file needs to be set `read-only`, to prevent parsec from modifying it.

- Ensure custom resolution data is set in `config.json`
- Right-click on `C:\ProgramData\Parsec\config.json` and open its Properties
- Check `Read-only`, apply and click OK
