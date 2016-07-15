# getkey

Command-line [Freedesktop.org Secret Service](https://specifications.freedesktop.org/secret-service/) client.

Tested against gnome-keyring.

### APT Depends:

* `python3-secretstorage`
* `xclip`

## `getkey`
Python command-line client using [secretstorage](https://github.com/mitya57/secretstorage)

List available keyrings:

    $ getkey --list-keyrings
    login
    foobar

Unlock a locked keyring if required, prompting for a password on stdin:

    $ getkey --keyring foobar --unlock
    ...

List keys from a given keyring:

    $ getkey --keyring foobar --list
    random1
    pw3

Retreive and print out the plaintext key:

    $ getkey --keyring foobar random1
    ...

Retreive a key into the X selection buffer, ready for pasting. Does not display the key:

    $ getkey --keyring foobar --selection pw3

Generate and store a new key, using `--generate-length` random alnum chars:

    $ getkey --keyring foobar --generate pw4

Output keynames for tab-completion:

    $ getkey --keyring foobar --list
    random1
    pw3
    $ getkey --keyring foobar --list ra*
    random1

## awesome `getkey.lua`
Support for Awesome using either `awful.prompt` with tab-completion or an interactive `awful.menu`.

Customize the keyring to use for the prompt:

    GETKEY_KEYRING = "foobar"

Bind to a key in your `~/.config/awesome/rc.lua` using:

    local getkey = require("awesome-getkey")

    globalkeys = awful.util.table.join(
        ...

        awful.key({ modkey },            "e",     function () getkey.prompt() end),
        awful.key({ modkey, "Shift" },   "e",     function () getkey.menu() end),

        ...
    )

## i3 `dmenu_getkey`

Trivial wrapper around `dmenu` and getkey, for use with i3.

    bindsym $mod+e exec --no-startup-id "dmenu_getkey"

