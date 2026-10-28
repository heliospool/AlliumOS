# AlliumOS

**Turn a Cheap Yellow Display into a Garlicoin miner.**

AlliumOS is firmware for the ESP32-2432S028R, the 2.8" "Cheap Yellow Display" (CYD). Flash it,
join it to your Wi-Fi, point it at a pool, and it mines Garlicoin around the clock, with
everything you want to know on its own screen and on a web page you can open from any device
on your network.

Think of it as a lottery ticket that never stops playing: a CYD does about 1,450 hashes a
second, so it shines on a pool that pays the miner who finds the block, such as
[HeliosPool](https://heliospool.com).

> This is a prerelease. It mines and runs steadily on our test board, but expect changes before 1.0.

## Features

**On the screen**
- Hashrate, shares accepted and rejected, and jobs from the pool, with icons that light up as
  work arrives and shares go out
- Hits: blocks you've found
- Best share this session and best ever
- Pool and network difficulty, block height, uptime, Wi-Fi signal and the board's address
- A scoreboard page with your best shares, your blocks, and how long a share and a block take
  on average
- A system page with the firmware, memory and network details
- A full-screen alert when you find a block

**On the web page**
- A live dashboard with a chart of your shares against the network difficulty, so you can
  see how close each one came to a block, and your hashrate over the last half hour
- Scoreboard: your ten best shares and your blocks, with dates and heights
- Logs: what the miner and the pool are saying, with a debug view for the details
- System: everything about the board at a glance
- Settings for everything, most of which apply the moment you save

**Mining**
- Works with any Stratum pool that mines Garlicoin
- A backup pool, used automatically if your main pool goes down
- Optional worker names
- Keeps your best shares and blocks across restarts

**Setup**
- First-time setup from your phone: the board shows a QR code for its setup network
- Wi-Fi, a custom hostname, automatic or static addressing, DNS, time server and time zone
- Screen brightness, timeout, refresh rate, colour inversion and rotation

## Getting started

### 1. Download

Open the [latest release](https://github.com/heliospool/AlliumOS/releases) and download the
**full** image, `alliumos-…-cyd-full.bin`.

### 2. Flash

Plug the board into your computer with a USB cable, then use a browser-based ESP32 flasher (in
Chrome or Edge):

1. Connect to the board's port.
2. Choose the **full** image you downloaded and set the address to **0x0**.
3. Flash, then press the board's reset button (or unplug it and plug it back in).

Prefer the command line? With [esptool](https://github.com/espressif/esptool):

    esptool.py --chip esp32 write_flash 0x0 alliumos-…-cyd-full.bin

### 3. Set it up

1. The board starts a Wi-Fi network called **AlliumOS-XXXX** and shows a QR code for it.
   Join it from your phone; the setup page opens by itself (or go to `http://192.168.4.1`).
2. Enter your Wi-Fi details, your pool (for example `grlc.heliospool.com:3341`), your
   Garlicoin address, and a worker name if you want one.
3. Save. The board joins your network and starts mining. Its address is shown at the top of
   the screen: open it in a browser to see the dashboard.

**Screen scrambled, blank or mirrored?** CYD boards come with one of two kinds of screen, and
AlliumOS starts out assuming the more common one. If yours is the other kind, set the board up
from your phone as above (that doesn't need the screen), then open the web page, go to
**Settings › Display**, choose the other panel, save, and restart.

## Updating

Each release also has an **app** image, `alliumos-…-cyd-app.bin`. Flash it at address
**0x20000** to update while keeping your Wi-Fi, pool, settings and records:

    esptool.py --chip esp32 write_flash 0x20000 alliumos-…-cyd-app.bin

Flashing a **full** image again starts over: it erases your settings and records.
