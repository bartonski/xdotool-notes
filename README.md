# `xdotool`


Associated tools

* `xwininfo` -- window information utility for X

    xwininfo -root -tree

    xwininfo -root -tree | egrep -v 'has no name|[0-9] child(|ren):' | cut -d \" -f 2 | sort | uniq -c

* `xprop`
* `xrandr`

## Choosing windows

### `xdotool search`

Search using various criteria

* --class       : Match against the window class.
* --classname   : Match against the window classname.
* --maxdepth N  : Set recursion/child search depth. Default is -1, meaning infinite. 0 means no depth, only root windows will be searched. If you only want toplevel windows, set maxdepth of 1 (or 2, depending on how your window manager does decorations).
* --name        : Match against the window name. This is the same string that is displayed in the window titlebar.
* --onlyvisible : Show only visible windows in the results. This means ones with map state IsViewable.
* --pid PID     : Match windows that belong to a specific process id. This may not work for some X applications that do not set this metadata on its windows.
* --screen N    : Select windows only on a specific screen. Default is to search all screens. Only meaningful if you have multiple displays and are not using Xinerama.
* --desktop N   : Only match windows on a certain desktop. 'N' is a number. The default is to search all desktops.
* --limit N     : Stop searching after finding N matching windows. Specifying a limit will help speed up your search if you only want a few results.  The default is no search limit (which is equivalent to '--limit 0')
* --all         : Require that all conditions be met. For example: `xdotool search --all --pid 1424 --name "Hello World"` This will match only windows that have "Hello World" as a name and are owned by pid 1424.
* --any         : Match windows that match any condition (logically, 'or'). This is on by default. For example: `xdotool search --any --pid 1424 --name "Hello World"` This will match any windows owned by pid 1424 or windows with name "Hello World"
* --sync        : Block until there are results. This is useful when you are launching an application and want to wait until the application window is visible.  For example:

    google-chrome &
    xdotool search --sync --onlyvisible --class "google-chrome"

#### `xdotool search` Examples:

Get window name from chromium:

    xdotool search --class "Chromium" getwindowname

### `behave`

    xdotool search --onlyvisible . behave %@ mouse-enter getwindowname

Note that the dot (.)  is significant.

Behave takes the folloing commands:

* `mouse-enter` : Like javascript 'mouse over'
* `mouse-leave` : Fires when the mouse leaves a window; operates on the window being left
* `mouse-click`: Like javascript 'on click'
* `focus` : Fires when the window gets input focus
* `blur` : Fires when the window loses focus

### `xdotool selectwindow`

    xdotool xdotool selectwindow getwindowname

### `getwindowfocus`

Prints the window id of the currently focused window. This would typically be used in a script; if you're working from the command line, the terminal you're in will most likely have focus.

### `getactivewindow`

This will shift to an active window on a different desktop, and is therefore more reliable than `getwindowfocus`

## Get information about a window 

* `getwindowname`
* `getwindowpid`
* `getwindowgeometry`
* `windowsize`
* `getmouselocation`

## Actions

* `mousemove` : `mousemove [options] x y OR 'restore'`
* `mousemove_relative`: `mousemove_relative [options] x y`
* `click`: `click [options] button`
* `mousedown`: Same as click, except only a mouse down is sent.
* `mouseup`: Same as click, except only a mouse up is sent.
* `windowmove`: `windowmove [options] [window] x y`
* `windowfocus`: Focus a window.
* `windowminimize`: `windowminimize [options] [window]`
* `windowraise`: Raise window to top.
* `windowkill`: Kill window
* `key`: `key [options] keystroke [keystroke ...]`
* `keydown`: Same as `key`, but only the key press event is sent.
* `keyup`: Same as `key`, but only the key up event is sent.
* `type`: Send a string of text.
* `sleep`:
* `exec`: 

# Examples

Select window and move it to a specified horizontal position

    xdotool selectwindow windowmove 1920 y

