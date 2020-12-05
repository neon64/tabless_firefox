# Patched Firefox

Original scripts from: https://github.com/nilcons/firefox-hacks

These two scripts [get_the_fox](./get_the_fox) and [patch_the_fox](./patch_the_fox)
can be used to patch the Firefox UI, for things like custom keyboard shortcuts.

Use at your own risk.

## Customization

You can inspect [browser.xhtml.patch](browser.xhtml.patch) to see what has been changed.

- `Ctrl+T` - open a new window instead of a new tab

Still to implement:

- `Ctrl+Click` - open link in new window instead of new tab

## Rationale

This is a very small part of my vendetta against application-specific tabs.
When using a window manager with built-in tabs support (i.e.: i3, sway, etc...),
I run Firefox with tabs disabled (using this patch, and also the
[tab-less addon](https://addons.mozilla.org/en-US/firefox/addon/tab-less-addon/)),
and use window manager tabs exclusively.

Also use a custom [userChrome.css](https://github.com/neon64/dotfiles/tree/master/.config/firefox) to hide the tab bar.

This has a number of benefits:

- Consistent keyboard shortcuts for tabs (I have bound Ctrl+[num] and Ctrl+Tab to change tabs, currently only implemented in my [sway fork](https://github.com/neon64/sway/))
- Window switchers (dmenu, wofi, rofi, etc...) will see each tab as a separate window, so you can switch to a new tab by searching for it, in the same you might switch to a new window by searching for it.


But also downsides:

- Opening a new window is anedcotally slightly slower than a new tab.
    - The [tab-less addon](https://addons.mozilla.org/en-US/firefox/addon/tab-less-addon/) by itself is painfully slow - it has to detect a new tab has been opened, then it moves it to a new window afterwards. This patch makes it faster
- No favicons for each website, instead each window just displays the Firefox logo.
  - This can theoretically be fixed:
    - on X11 there is a way to change the application's icon dynamically
    - on Wayland, application icons are retrieved from the `.desktop` files, we would need a new extension in order to override this
  - As a workaround you can override the `title` of certain sway/i3 windows to include an icon of your choice.