First public release of the SD-free local firmware for the GNCC GC2 (Anyka AK3918EV, JXF37 sensor).

Runs entirely from internal flash — no SD card, no cloud, no app.

## Features
- **RTSP** streaming — main 1280×720 (`/vs0`) + sub 640×480 (`/vs1`)
- **Automatic day/night** via the ISP's native auto-switch — no pink cast, no oscillation, works indoors where light changes at any hour
- **Grayscale night** vision (IR-cut + IR LED + ISP night profile)
- **Web UI** (port 80) — live JPEG preview, day/night control, status, stream links (Thingino-inspired)
- **Wi-Fi**, **telnet** (maintenance), front **LED off**

## Key technical solutions (see README)
- Day/night: `ak_vpss_isp_get_auto_day_night_level` with **complete** threshold arrays
- Night pink fix: `ak_vi_switch_mode(VI_MODE_NIGHT)`
- Live preview: `ak_vi_get_frame` + `ak_venc_send_frame` (one-shot, avoids the ISP crash from `request_stream`)
- SD-free install: rebuilt XZ `/usr` squashfs, flashed from U-Boot

## Install
See [INSTALL.md](INSTALL.md). **Requires a serial console** for U-Boot access and recovery. Flashing SPI-NOR can brick the device — back up the stock `/usr` first.

## Notes
- The Anyka SDK libraries are proprietary and **not** included — extract them from your own firmware (see `src/README.md`).
- Tested on the GNCC GC2 (OSAIO/Nooie variants share the hardware).

Credits: [Thingino](https://thingino.com/) (web UI inspiration), [piotr-go](https://github.com/piotr-go/GNCC_GC2_ak3918ev300_RTSP) (U-Boot flash method + day/night arrays), and the Anyka hacking community.
