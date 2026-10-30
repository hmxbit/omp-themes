# Repository guide

- Root `*.omp.json` files are independent Oh My Posh configurations. Older themes use version 3 and `properties`; newer ones use version 4 and `options`. Preserve each file's existing style unless migration is requested.
- `preview.html` is a standalone, hand-written mockup, not generated from the JSON. Its Git toggle changes example state only. Update the relevant card manually when asked to keep a preview in sync.
- Git branch icons use the Nerd Font glyph `` (`U+E725`); terminal and browser rendering depends on the configured fonts.
- To apply a theme in Zsh, use `eval "$(oh-my-posh init zsh --config ~/omp-themes/harbor.omp.json)"` in `~/.zshrc`, replacing the filename as needed. Reload with `source ~/.zshrc` or open a new shell.

## Verification

- Check JSON syntax: `for f in *.omp.json; do python3 -m json.tool "$f" >/dev/null || exit 1; done`
- Render one theme with Oh My Posh: `env -u POSH_CONFIG -u POSH_SESSION_ID oh-my-posh print primary --config "$PWD/harbor.omp.json" --plain --shell zsh --execution-time 1200`. Replace the filename for another theme; omit `--plain` to inspect colors. Clearing those variables avoids rendering the active shell's cached configuration instead of the selected file.
- Git and language segments are context-dependent. Exercise a theme from an actual Git repository and, for Node, Go, or Python segments, a directory containing `package.json`, `go.mod`, or a `.py` file respectively; also check outside those contexts. Use an absolute config path when changing directories. The execution-time segments appear only for commands taking at least 500 ms.
