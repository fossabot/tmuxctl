# tmuxctl

Tmuxctl is a tmux session manager. Read the [documentation](https://tmuxctl.netlify.com/) for instructions and examples.

## Quick start

Install Tmuxctl:
```
$ curl -sf https://raw.githubusercontent.com/alexandrebodin/tmuxctl/master/install.sh | sh
```

Create a `.tmuxctlrc` file:
```toml
name = "tmuxctl_test"
dir = "~/"

# selects the window to start in
select-window = "docker" 
# selects the pane to start in.
# must select a window  first, otherwise ignored
# first panel is 1 and so on...
# select-pane = 3

# option to clear panes after init
clear-panes=true

# run scripts just after window is initialised
# and before panes are created
window-scripts=[
  "date"
]

[[windows]]
  name="docker"
  dir="~/dev/some-folder"
  # synchronize panes
  # sync=true

  # runs in the inital window before panes creation
  scripts=[ "touch test.text" ]

  # runs in each pane before pane's own scripts
  pane-scripts=[ "echo new pane" ]

  # select window-layout
  # layout="tiled"

  [[windows.panes]]
    dir="~/dev/some-folder"
    # start session with this pane zoomed
    # zoom=true
  [[windows.panes]]
    # split horizontally and take full height
    split="-h -p 50" 
  [[windows.panes]]
    scripts=[ "echo hi" ]

[[windows]]
  name="some-extra-window"
```

Start your tmux session:
```
$ tmuxctl
```