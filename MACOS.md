# Updating MacOs TermInfo
MacOs provides an outdated version of [ncurses](https://en.wikipedia.org/wiki/Ncurses), which does not contain details for dealing with `tmux-256color` terminfo. This can cause issues like making the `DEL` key not delete anything.

This can be solved by generating the terminfo ourselves with a new version of ncurses provided by hombrew/macports. The steps are as follow below. Props to [Gregory](https://gpanders.com/blog/the-definitive-guide-to-using-tmux-256color-on-macos/) for sharing this solution.

## Generate tmux terminfo
```
XTERM_INFO_SRC_PATH="$HOME/tmux-256color.src"
# MacPorts
$ /opt/local/bin/infocmp -x tmux-256color > $XTERM_INFO_SRC_PATH

# Homebrew
$ /usr/local/opt/ncurses/bin/infocmp -x tmux-256color > $XTERM_INFO_SRC_PATH
```

## Patch the tmux terminfo
```
sed -i 's/pairs#0x10000/pairs#32767/' $XTEMR_INFO_SRC_PATH
ed -i 's/pairs#65536/pairs#32767/' $XTEMR_INFO_SRC_PATH
```

## Install terminfo for our user
```
USER_TERMINFO_DIRS=$HOME/.local/share/terminfo
/usr/bin/tic -x -o $USER_TERMINFO_DIRS $XTEMR_INFO_SRC_PATH
```

## Export it into your zshrc/bashrc
Adds the following line to the rc file of your shell.
```
export TERMINFO_DIRS=$TERMINFO_DIRS:$HOME/.local/share/terminfo
```
