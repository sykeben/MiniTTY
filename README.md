# MiniTTY

A little full-duplex soundcard "modem" emulator that relies on [`minimodem`](https://github.com/kamalmostafa/minimodem).

---

### Requirements

* A relatively modern linux distro with `bash` or `ksh` installed.
* Read/write access to `/tmp`.
* A soundcard with audio output and input support.
* An installation of [`minimodem`](https://github.com/kamalmostafa/minimodem).

---

### Installation

1. Clone this repo or download it as a `zip` archive.
2. Navigate to your downloaded copy.
3. Make `minitty` executable with `chmod +x minitty`.
4. Copy `minitty` to wherever you want.

---

### Usage

`./minitty [options]`

By default, MiniTTY behaves like an American TTY/TDD.

The syntax for `[options]` is identical to that of [`minimodem`](https://github.com/kamalmostafa/minimodem)'s, with a few exceptions:

1. Do not use `--tx` or `--rx` as MiniTTY uses them on its own to set up the TX and RX processes.
2. Do not use `--quiet` as it is used by default on the RX process.
