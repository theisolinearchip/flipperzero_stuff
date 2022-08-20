# A bunch Flipper Zero apps and random tinkering...

Some things [Flipper Zero](https://github.com/flipperdevices/flipperzero-firmware)-related I've been working on (mostly standalone plugins and applications)

## Apps

Under the `/applications` folder there's a (small) collection of different apps:

- `MultiConverter`, a multi-unit converter written with an easy and expandable system for adding new units and conversion methods (it has it's own [README file](https://github.com/theisolinearchip/flipperzero_stuff/tree/main/applications/multi_converter) with more info)
- `Dec/Hex Converter`, a decimal to hexadecimal (and vice versa) converter with "real-time" conversion and built-in keyboard ([some pics here!](https://twitter.com/isolinearchip/status/1553824011620073472)). Updates on this one will be probably stopped since the __MultiConverter__ covers
this scenario (and lots more with more units!)
- `Conway's Game of Life`, simple implementation on a full-screen 32 x 16 cell grid ([video and pics here!](https://twitter.com/isolinearchip/status/1553094272961974272))

Each app can be added as a __plugin__ on a regular [flipperzero firmware source](https://github.com/flipperdevices/flipperzero-firmware):

1. Copy the plugin folder (ex: `/applications/game_of_life`) to the main `/applications` one
2. Modify the `/applications/meta/application.fam` main manifest and add the plugin entry in the proper section:

```
App(
    appid="basic_plugins",
    name="Basic applications for plug-in menu",
    apptype=FlipperAppType.METAPACKAGE,
    provides=[
        "music_player",
        "snake_game",
        "bt_hid",
        "game_of_life", // <<--- here's the new definition (use the appid from the app application.fam manifest)
    ],
)
```

3. Compile the firmware and install

## Firmware build

I usually use a standard __updater_package__ build that creates an executable file I can push to my Flipper and run it as a new update:

```
$ ./fbt --with-updater COMPACT=1 DEBUG=0 VERBOSE=1 updater_package
```

(this requires all the proper dependencies, check the docs from the official repo for more info!)

## Notes

- The `order` option on the `application.fam` for each app sets the _priority order_ on the menu list
- Nope, currently it's not possible to "install apps" without reflashing the entire firmware with everything inside :(
- My idea is to keep everything here up-to-date with the new firmware releases, so let me know if something doesn't work or anything related!
- To work on a full __flipperzero source folder__ while having my stuff in my own repo I like to create symlinks to the folders inside the `/applications` main dir:
```
~/flipper_zero/flipperzero-firmware/applications$ ln -s ~/flipper_zero/flipperzero_stuff/applications/dec_hex_converter/ dec_hex_converter
~/flipper_zero/flipperzero-firmware/applications$ ln -s ~/flipper_zero/flipperzero_stuff/applications/game_of_life/ game_of_life

and so on...
```

## Links and references

- [Official firmware](https://github.com/flipperdevices/flipperzero-firmware)
- [Hello World Tutorial](https://github.com/DroomOne/Flipper-Plugin-Tutorial), I used this one as the starting point for my firsts projects. It may be a
little bit outdated, but combined with any other "current" app (like the _Snake minigame_) it should be more than enough to start tinkering with the system.

## Contact

You can reach me on [twitter](https://twitter.com/isolinearchip), [instagram](https://instagram.com/theisolinearchip) or by [mail](mailto:albert.gonzalez.fdez-at-gmail-dot-com)
