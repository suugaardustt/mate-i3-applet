# MATE i3 Workspace Applet

![screenshot](https://raw.github.com/city41/mate-i3-applet/master/screenshot.png)

This applet shows the current state of i3 workspaces when using i3 as your window manager in MATE.

## Features
1. shows all workspaces in a similar fashion as i3bar
2. urgent workspaces highlight same as i3bar
3. clicking a workspace goes to that workspace
4. uses the same colors as your i3bar in your i3 config (see below)
5. robust, reconnects if i3 relaunches

## Tested On

* Ubuntu MATE 16.04 with MATE 1.12.1 and i3 4.11
* Ubuntu MATE 17.10 with MATE 1.18.0 and i3 4.13 (see caveat just below)

## Using on MATE 1.18.0+

MATE 1.18.0 made the switch to GTK 3, and so this applet does not work. I'll address that properly eventually, but to fix it, edit matei3applet.py. Towards the top, change

`gi.require_version("Gtk", "2.0")`

to

`gi.require_version("Gtk", "3.0")`

## How to Install

Requires Python 3, no other dependencies

1. Grab the most recent [release](https://github.com/city41/mate-i3-applet/releases)
2. `sudo ./setup.py install`
3. `killall mate-panel` - this should kill then bring mate panel back, and it will now know about the i3 applet
4. Right click a panel, choose 'Add to panel...' and add the i3 applet

## How to setup i3 for this applet

The point of this applet is to use a MATE panel instead of an i3 bar. But, this applet also reads your bar config to determine the colors to use. This is not a catch-22, as i3 allows you to define invisible bars. So in your i3 config, define one bar like so:

```
bar {
    tray_output None
    mode invisible
    colors {
        background #000000
        statusline #ffffff
        separator #666666

        focused_workspace  #4c7899 #285577 #ffffff
        active_workspace   #333333 #5f676a #ffffff
        inactive_workspace #333333 #222222 #888888
        urgent_workspace   #2f343a #900000 #ffffff
        binding_mode       #2f343a #900000 #ffffff
    }
}
```

`tray_output None`: tells the bar to not accept tray icons. This allows them to go to the MATE panel.

`mode invisible`: means the bar is invisible and never shown. We really only want the bar for its colors...

`colors`: define the colors you want here. The applet will use these colors. Check the [i3 user guide](https://i3wm.org/docs/userguide.html#_colors) for more info on how to specify colors.

### If you just want default colors

If you don't define a bar, or your bar doesn't have any colors defined, then the applet will use i3's default colors. Incidentally, the bar example above is what the default colors are.

## Todo

Check the github issues, tracking all known issues and work there

## License

This applet is using the BSD license. I also copied i3-ipc's source over into this applet because I needed the latest version and its not yet published ti PyPI. i3-ipc is also licensed under the BSD license.
