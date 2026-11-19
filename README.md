# setbrowser

List and switch your default browser on macOS. Uses built-in macOS tools, with no dependencies to install.

## Install

```sh
git clone https://github.com/jhinds/setbrowser.git
cd setbrowser
mkdir -p "$HOME/.local/bin"
install -m 755 setbrowser "$HOME/.local/bin/setbrowser"
```

Make sure `~/.local/bin` is on your PATH. If needed, add this line to `~/.zshrc` and open a new terminal:

```sh
export PATH="$HOME/.local/bin:$PATH"
```

## Usage

```sh
setbrowser                  # List available browsers
setbrowser --list           # Same list
setbrowser chrome           # Set Chrome as the default
setbrowser firefox          # Set Firefox as the default
setbrowser safari           # Set Safari as the default
setbrowser finicky          # Set Finicky as the default
setbrowser --current        # Show HTTP and HTTPS defaults
setbrowser --dry-run chrome  # Preview without changing anything
setbrowser --help           # Show help
```

The list is discovered from installed apps registered with macOS, rather than a fixed list of browser names. Apps must support HTTP, HTTPS, and HTML documents. An asterisk marks the current HTTPS default.

Names are case-insensitive. You can use a short name, a full name, a bundle ID, or an unambiguous partial name:

```sh
setbrowser "Google Chrome"
setbrowser com.google.Chrome
```

Ambiguous or unknown names fail without changing anything. If two browsers share a short name, use the full name or bundle ID shown in the error.

## Notes

- Sets both HTTP and HTTPS defaults for the current user.
- macOS may ask you to confirm the change.
- Chooses the browser app, not a browser profile.
- Runs through `/usr/bin/osascript` and Apple's AppKit and CoreServices frameworks. It currently uses Apple's older Launch Services functions.

If Claude sign-in opens Safari while Finicky is the default, try `setbrowser chrome`, complete sign-in, then run `setbrowser finicky` to restore it.

## Verify

Run `setbrowser --list`, `setbrowser --current`, and `setbrowser --dry-run chrome` to check browser discovery and name matching without switching browsers.
