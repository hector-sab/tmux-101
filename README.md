# Tmux 101
Welcome to tmux 101! In this guide I'll attempt to show you all the basics you need to feel comfortable
using tmux.

> **&#9432;** **NOTE:** The keyboard is the primary way of using tmux. If you are more interested on using
your mouse, keep reading as it's possible to some extent. However, I'd recommend letting go and embrase
your fingers. Lots of things will become easier once you have built enough muscle memory.

> **&#9432;** **NOTE 2:** If you are in MacOs, take a look at this [extra steps](MACOS.md).

## Installation
You can refer to the [tmux wiki](https://github.com/tmux/tmux/wiki/Installing) for the most up to date
information on how to install it on your system.

## Basics

#### Open tmux
Typing `tmux` and pressing `Enter` on a terminal should be enough to start tmux.
```bash
$ tmux
```

#### Create a window (a.k.a. tab)
Once inside tmux, it's possible to create windows/tabs. For that, you need to:
- press the key `control`
- without releasing `control`, press `b` and release both keys
- press `c`

Such key binding is also expressed as below
```
C-b + c
```

You can achieve the same result by doing
```
C-b + :new-window
```

#### Rename a window
By default, the window is dynamically named after the command that it's running. If
we know already that we will dedicate a window to something in particular, it's possible
to rename it with the following command.
```
C-b + ,
```

#### Create panes
In case there's a need to see more than one terminal at the same time, it's possible
to make a vertical split using the key binding below.
```
C-b + %
```

Prefer a horizontal split? Tmux got you.
```
C-b + "
```

#### Prefix
As you have seen, `C-b + <key>` for contrlling tmux behavior. `C-b` (referred to as `Ctrl-b` in some places) is also
known as `<prefix>` and it can be configured to be anything.

> **&#9432;** **NOTE:** If you ask me, it's better to keep the default prefix.
This way you can use tmux on other systems without having to struggle with your
muscle memory.

#### Move across panes
Move up, down, left, or right using the arrows of your keyboard.
```
<prefix> + <arrow>
```

#### Move across windows
Move to the right, or next, window.
```
<prefix> + n
```

Move to the left, or previous, window.
```
<prefix> + p
```

Move to a specific window.
```
<prefix> + <number>
```

#### Sessions
Let's say that it's now time to work on a different project, but the current terminals
open are still of use. Instead of adding a new window, tmux is capable of creating new
sessions, or "fresh spaces". To make a new session

```
<prefix> + :new-session
```

It's also possible to assign a name
```
<prefix> + :new-session -s my-session-name
```

or to rename the current session.
```
<prefix> + :rename-session my-session-name
```

#### Change active session
```
<prefix> + s
```

or
```
<prefix> + :choose-session
```

#### Show pane title
Show pane titles
```
<prefix> + :set pane-border-status top
```

Change name of the pane
```
<prefix> + :select-pane -T my-pane-title
```

## Mouse mode
Enable the mouse mode by setting the `mouse` option to `on`. Now try right clicking around
the terminal to see what the options are. Hint: right click on the session indicator and
on the window names. You can also change the focused window/pane by clicking on them, or
resize panes by drag and dropping their edges. Disable it by setting it to `off`.
```
# Turn mouse on
<prefix> + :set mouse on

# Turn mouse off
<prefix> + :set mouse off
```

## Quality of life
These are configurations I like to have setup.

#### Set index starting from 1
These two options allow you to change the start number of the index assigned to
all windows and panes on tmux.
```
set -g base-index 1
set -g pane-base-index 1
```
I find this index numbering useful when changing quickly to a different pane (`<prefix> + q + <pane-index-number>`) or window (`<prefix> + <window-index-number>`).

Take a look at the screenshots below. The image on the left shows the
default behavior, and the one in the right has the setting from above enabled.
You will notice how both pane and window indexes start from either zero (left) or one (right).

![](media/tui-indexes-default.png)  |  ![](media/tui-indexes-1-based.png)
:-------------------------:|:-------------------------:
Zero-base index             |  One-base index


> **&#9432;** **NOTE:** The session "index" shown when doing `<prefix> + s` cannot
be changed to be 1-based as what's shown is in reality the session id, and the
maintainers seem to be unwilling to add an index here.

#### Attach to another session after closing last window
This option allows tmux to change to a different session in case you close all
the windows/panes of the current one. If not enabled, it will detach from tmux
and will require you to manually attach to any of the existing sessions.

```
set -g detach-on-destroy no-detached
```

#### Disable bell sounds
As the title suggests, disables tmux from making unrequested noises.

```
set -g bell-action none
```

#### Create new windows with current working directory
When creating new windows the default path used for the new terminal is the one
from where tmux was opened. This makes sure that any new window is created at
the path of the current active pane.

```
bind c new-window -c "#{pane_current_path}"
```

#### Split panes with current working directory
By default, tmux creates new panes at the path where tmux was first executed. This
makes sure to create panes using the current active pane's path.

```
bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
```

#### Increase history
Allow tmux to store more lines in the buffer of each pane.
```
set -g history-limit 50000
```

This option is useful if you like scrolling back to a few minutes/hours back in the past to see what was typed in the terminal and what was the output.

## Custom quality of life
#### Custom pane titles
Bash scripts at `dotfiles/.local/bin`.

# Other resources
The official tmux wiki page has lots of information on how to use tmux that I'd recommend checking out:
- [Getting started](https://github.com/tmux/tmux/wiki/Getting-Started)
- [Clipboard](https://github.com/tmux/tmux/wiki/Clipboard)
- [FAQ](https://github.com/tmux/tmux/wiki/FAQ)
- [Advanced use](https://github.com/tmux/tmux/wiki/Advanced-Use)
