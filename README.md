# lgpio Python Wheels

Pre-built Python wheels for the [lgpio](http://abyz.me.uk/lg/py_lgpio.html) library on aarch64 (ARM64) Linux, targeting Raspberry Pi 5 and other 64-bit ARM single-board computers.

## Why?

The upstream [lgpio package on PyPI](https://pypi.org/project/lgpio/) only provides a source distribution that requires `swig`, `python3-dev`, and the `liblgpio` C library to build. This makes `pip install lgpio` fail on most systems without those build dependencies.

These wheels are statically linked and self-contained — no system libraries or build tools needed.

## Available Wheels

| Wheel | Python | Architecture | Platform |
|---|---|---|---|
| `lgpio-0.2.2.0-cp313-cp313-linux_aarch64.whl` | 3.13 | aarch64 | Linux ARM64 |
| `lgpio-0.2.2.0-cp314-cp314-linux_aarch64.whl` | 3.14 | aarch64 | Linux ARM64 |

## Installation

### Using `--find-links` (recommended)

```bash
pip install lgpio --find-links https://github.com/makermelissa/lgpio-python-wheels/raw/main/wheels/
```

### Direct URL install

```bash
# Python 3.13
pip install https://github.com/makermelissa/lgpio-python-wheels/raw/main/wheels/lgpio-0.2.2.0-cp313-cp313-linux_aarch64.whl

# Python 3.14
pip install https://github.com/makermelissa/lgpio-python-wheels/raw/main/wheels/lgpio-0.2.2.0-cp314-cp314-linux_aarch64.whl
```

### Alternative: apt (Raspberry Pi OS only)

On Raspberry Pi OS (Bookworm/Trixie), lgpio is available as a system package:

```bash
sudo apt-get install -y python3-lgpio
```

## Building Wheels

These wheels were built on a Raspberry Pi 5 running Raspberry Pi OS Trixie (Debian 13) with the `PYPI=1` flag for static linking:

```bash
# Install build dependencies
sudo apt-get install -y swig python3-dev

# Download lgpio source
pip download --no-binary :all: --no-deps lgpio==0.2.2.0
tar xzf lgpio-0.2.2.0.tar.gz
cd lgpio-0.2.2.0

# Build statically linked wheel
PYPI=1 pip wheel . --no-deps --no-build-isolation -w wheels/
```

## Related

- [lgpio homepage](http://abyz.me.uk/lg/py_lgpio.html)
- [Adafruit Blinka](https://github.com/adafruit/Adafruit_Blinka) — CircuitPython API for SBCs
- [Adafruit Blinka issue #1016](https://github.com/adafruit/Adafruit_Blinka/issues/1016) — lgpio install errors on Pi 5

## License

The lgpio library is released under the [Unlicense](http://unlicense.org/). The wheel packaging in this repository is provided under the MIT License.
