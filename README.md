# Cross-platform pbcopy

Cross-platform pure POSIX shell implementation of the macOS utility `pbcopy`.
Pipe text to it to put that text on your system clipboard.

It works almost anywhere shell scripts can run (including local and remote Linux
hosts, and tmux sessions), provided your terminal emulator supports
the OSC52 escape sequence:

    macos $ scp pbcopy linuxserver:
    macos $ ssh linuxserver
    linux $ chmod +x pbcopy
    linux $ echo "foobar" | pbcopy
    linux $ exit
    macos $ pbpaste
    foobar

Terminal emulators that support OSC52 include at least iTerm2 (enable
"Applications in terminal may access clipboard" in Preferences) and alacritty.

## Installation

Place `pbcopy` on your `$PATH`, e.g.

    curl https://raw.githubusercontent.com/mikepqr/pbcopy-sh/main/pbcopy -o ~/.local/bin/pbcopy && \
      chmod +x ~/.local/bin/pbcopy

It's effectively a one-liner, but I wrapped it up in a very short script to make
distribution and documentation easier.

## Limitations

Doesn't work inside neovim's terminal emulator (#3) or containers (#4)

## Alternatives

- [skaji/remote-pbcopy-iterm2](https://github.com/skaji/remote-pbcopy-iterm2)
  (go binary with perl and python alternatives)
- [bottlerocketlabs/remote-pbcopy](https://github.com/bottlerocketlabs/remote-pbcopy)
  (fork of skaji/remote-pbcopy-iterm2, works in neovim's terminal emulator)
- [osc52.sh](https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/osc52.sh)
  (shell script for chromium OS)
- `xclip -selection clipboard` (X11/Linux only, requires 5MB of dependencies)

## References

- [Chromium
  OS](https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/FAQ.md#Is-OSC-52-aka-clipboard-operations_supported)
- [tmux in practice: integration with system
  clipboard](https://www.freecodecamp.org/news/tmux-in-practice-integration-with-system-clipboard-bcd72c62ff7b/)
- [Copying to clipboard from tmux and Vim using OSC
  52](https://sunaku.github.io/tmux-yank-osc52.html)
