# TermuxPP:Boot

A TermuxPP add-on app to run programs when the device boots.

> **TermuxPP release channel:** New builds are published in the
> [TermuxPP monorepo](https://github.com/pschmitt/termuxpp/releases/tag/latest).
> Existing releases here remain available to older clients. See the
> [self-update guide](https://github.com/pschmitt/termuxpp/blob/main/docs/en/self-update.md).

This fork keeps the upstream Java namespace (`com.termux.boot`) and uses the
TermuxPP Android package `dev.pschmitt.termux.boot`. It shares the UID and
signing certificate of the TermuxPP core (`dev.pschmitt.termux`).

## Installation

Install the TermuxPP:Boot APK built for TermuxPP. It is not interchangeable
with upstream Termux:Boot or an APK signed with a different key.

## How to use

1. Install TermuxPP:Boot.
2. Open it once after installation. Android requires this before it will
   deliver boot broadcasts to the app.
3. Put executable scripts in `~/.config/termuxpp/boot/`.
4. Scripts run in filename-sorted order. If the same filename exists in
   multiple supported directories, only the first is used, following this
   per-file precedence order:
   - `~/.config/termuxpp/boot/` (preferred)
   - `~/.config/termux/boot/` (legacy XDG location)
   - `~/.termux/boot/` (legacy location)

   Different filenames from all three directories are retained. A script in a
   higher-priority directory replaces only a lower-priority script with the
   same filename.
5. Consider running `termux-wake-lock` first if the device should be kept awake.

For example, create `~/.config/termuxpp/boot/start-sshd`:

```sh
#!/data/data/dev.pschmitt.termux/files/usr/bin/sh
termux-wake-lock
sshd
```

## License

Released under [the GPLv3 license](https://www.gnu.org/licenses/gpl.html).
