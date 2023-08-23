# Tmux 101
Welcome to tmux 101! In this guide I'll show you the basics of how to navigate it and don't die trying.

## Installation

## Basics

#### Open tmux

```bash
$ tmux
```

#### Create a window (a.k.a. tab)
Once inside tmux, it's possible to create tabs/windows. For that you need to:
- press the key `control`
- without releasing press `b`, followed by releasing both keys
- press `c`

Such keybinding is also expressed as below.
```
C-b + c
```

#### Rename a window
By default, the window is dynamically named after the command that it's running. If
we know already that we will dedicate that window to something in particular, it's possible
to rename it with the following command.
```
C-b + ,
```

#### Create panes
In case there's a need to see more than one terminal at the same time, it's possible
to make a vertical split using the keybinding below.
```
C-b + %
```

Prefer a horizontal split? Tmux got you.
```
C-b + "
```

#### Prefix
As you have seen, `C-b + <key>` for contorling tmux behavior. `C-b` (refered to as `Ctrl-b` in some places) is also
known as `<prefix>` and it can be configured to be anything.

> **&#9432;** **NOTE:** If you ask me, it's better to keep the default prefix.
This way you can use tmux on other systems without having to struggle with your
muscle memory.

#### Sessions
Let's say that it's now time to work on a different project, but the current terminals
open are still of use. Instead of adding a new window, tmux is capable of creating new
sessions, or "fresh spaces". To make a new session

```
<prefix> + :new-session
```

It's also possible to assign a name.
```
<prefix> + :new-session -s my-session-name
```

## Customs
