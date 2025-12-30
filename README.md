# KMSCON

Kmscon is a simple terminal emulator based on linux kernel mode setting (KMS).
It is an attempt to replace the in-kernel VT implementation with a userspace
console. See kmscon(1) man-page for usage information.

## ARMBIAN BUILD

```bash
git clone https://github.com/NickAlilovic/kmscon.git
cd kmscon
git archive --prefix=kmscon-9.2.1/ -o ../kmscon_9.2.1.orig.tar.gz HEAD
dpkg-buildpackage -us -uc
```

## Requirements

Kmscon requires the following software:
  - **[libtsm](https://github.com/NickAlilovic/libtsm)**: terminal emulator state machine
  - [libudev](https://www.freedesktop.org/software/systemd/man/libudev.html): providing input, video, etc. device hotplug support (>=v172)
  - [libxkbcommon](https://xkbcommon.org/): providing internationalized keyboard handling
  - [libdrm](https://gitlab.freedesktop.org/mesa/drm): graphics access to DRM/KMS subsystem
  - linux-headers: linux kernel headers for ABI definitions

Everything else is optional:

For video output at least one of the following is required:
- fbdev: For framebuffer video output the kernel headers must be installed and located in the default include path.
- DRM: For unaccelerated drm output the "libdrm" library must be installed and accessible via pkg-config.
- OpenGLES2: For accelerated video output via OpenGLESv2 the following must be installed: libdrm, libgbm, egl, glesv2 (i.e., mesa)

For font handling the following is required:
- 8x16: The 8x16 font is a static built-in font which does not require external dependencies.
- unifont: Static font without external dependencies.
- pango: drawing text with pango Pango requires: glib, pango, fontconfig, freetype2 and more

