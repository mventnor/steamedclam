# steamedclam

A tiny `caffeinate -d`-style CLI for macOS. While it's running, the lid
can be closed without the machine sleeping. When it exits, normal
lid-close sleep is restored.

It is a signal-aware wrapper around:

```bash
sudo pmset -a disablesleep 1   # on start
sudo pmset -a disablesleep 0   # on exit
```

## Why?

`caffeinate -d` prevents *display* sleep but the system still sleeps when
the lid is closed. The real toggle for that is `pmset … disablesleep`,
which needs root. Running `steamedclam` under `sudo` once avoids
repeated password prompts and guarantees sleep is re-enabled on exit
(Ctrl+C, SIGTERM, SIGHUP, or normal termination).

## Install

```bash
chmod +x ~/steamedclam/steamedclam
sudo ln -s ~/steamedclam/steamedclam /usr/local/bin/steamedclam   # optional
```

## Usage

```bash
sudo steamedclam
```

Press `Ctrl+C` (or send `SIGTERM`) to re-enable lid-close sleep and exit.
