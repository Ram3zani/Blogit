## Tmux
For base funtionality install tmux:
`sudo pacman -S tmux `

## Save/restore sessions
For restore tmux environment after system restart we need a plugin called `tmux-resurrect`. But before to use it we need to install tpm(tmux-plugin-manager).

### Install tmp(tmux-plugin-manager)
Requirements: `tmux` version 1.9 (or higher), `git`, `bash`.

Clone TPM:

```bash
$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Put this at the bottom of `.tmux.conf`:

```bash
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

Reload TMUX environment so TPM is sourced:

```bash
# type this in terminal if tmux is already running
$ tmux source ~/.tmux.conf
```

That's it!

### Install tmux-resurrect

Add plugin to the list of TPM plugins in .tmux.conf:

`set -g @plugin 'tmux-plugins/tmux-resurrect'`

And use it:
```
prefix + Ctrl-s - save
prefix + Ctrl-r - restore
```

## Start tmux on every shell login
After install tmux-resurrect you must add some line of codes to .bashrc/.zshrc(before aliases). but before do it instal a little package called: `xdotool` that automate hitting CTRL+a CTRL+r for us every time we login to new session:

`sudo pacman -S xdotool`
```
# TMUX
if which tmux >/dev/null 2>&1; then
    #if not inside a tmux session, and if no session is started, start a new session
    test -z "$TMUX" && (tmux attach || tmux new-session)
    xdotool key CTRL+a CTRL+r
fi
```

Sources
----
* [tmux](https://wiki.archlinux.org/index.php/tmux)
* [everything-you-need-to-know-about-tmux-copy-pasting](http://www.rushiagr.com/blog/2016/06/16/everything-you-need-to-know-about-tmux-copy-pasting-ubuntu/)
* [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect)
* [tpm](https://github.com/tmux-plugins/tpm)