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

**`./minitty [options]`**

By default, MiniTTY behaves like an American TTY/TDD.

The syntax for `[options]` is identical to that of [`minimodem`](https://github.com/kamalmostafa/minimodem)'s, with a few exceptions:
1. Do not use `--tx` or `--rx` as MiniTTY uses them on its own to set up the TX and RX processes.
2. Do not use `--quiet` as it is used by default on the RX process.

---

### How it Works

MiniTTY is essentially a wrapper that launches two [`minimodem`](https://github.com/kamalmostafa/minimodem) instances (one for TX, one for RX) and slams the TX's input and RX's output together in one console.

**The Process: MiniTTY...**
 1. Gets user-selected options for both [`minimodem`](https://github.com/kamalmostafa/minimodem) instances (or default to `tdd` if nothing is supplied).
 2. Opens/creates a pipe for data being sent to the TX process: `/tmp/minitty_tx_[id]`.
 3. Launches the TX process, pipes its input in from the TX pipe, and saves its PID.
 4. Opens/creates a pipe for data being recieved from the RX process: `/tmp/minitty_rx_[id]`.
 5. Launches the RX process, pipes its output out to the RX pipe, and saves its PID.
 6. Connects the console's input and output to the RX and TX pipes, respectively.
 7. **Waits for the user to strike CTRL+C.**
 8. Closes the console's connections to both pipes.
 9. Kills the RX process using the PID from earlier.
10. Closes/deletes the pipe used for recieving RX data.
11. Kills the TX process using the PID from earlier.
12. Closes/deletes the pipe used for sending TX data.

It's an incredibly basic concept that seems to work well enough for my purposes, hence why MiniTTY is contained entirely within a single shell script.
