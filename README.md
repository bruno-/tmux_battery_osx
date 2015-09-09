# Tmux battery status

Enables displaying battery percentage and status icon in tmux status-right.

Battery full (for OS X):<br/>
![battery full](/screenshots/battery_full.png)

Battery discharging, custom discharge icon:<br/>
![battery discharging, custom icon](/screenshots/battery_discharging.png)

Battery charging:<br/>
![battery charging](/screenshots/battery_charging.png)

Battery remain:<br/>
![battery remain](/screenshots/battery_remain.png)

This is done by introducing new format strings that can be added to
`status-right` option:
- `#{battery_icon}` - will display a battery status icon
- `#{battery_percentage}` - will show battery percentage
- `#{battery_remain}` - will show remaining time of battery charge
- `#{battery_graph}` - will show battery percentage as a bar graph ▁▂▃▅▇
- `#{battery_prefix}` & `#{battery_suffix}` - allows formatting (e.g. colors)
  to be applied based on the current battery level

### Usage

Add `#{battery_icon}`, `#{battery_percentage}`, `#{battery_remain}` or `#{battery_graph}` format
strings to existing `status-right` tmux option. Example:

    # in .tmux.conf
    set -g status-right 'Batt: #{battery_icon} #{battery_percentage} #{battery_remain} | %a %h-%d %H:%M '

To add formatting based on the current charge status, add the
`#{battery_prefix}` and `#{battery_suffix}` strings. Example:

    # in .tmux.conf
    set -g status-right "Batt: #{battery_prefix}#{battery_icon} #{battery_percentage}#{battery_suffix} | %a %h-%d %H:%M "

### Installation with [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm) (recommended)

Add plugin to the list of TPM plugins in `.tmux.conf`:

    set -g @plugin 'tmux-plugins/tmux-battery'

Hit `prefix + I` to fetch the plugin and source it.

If format strings are added to `status-right`, they should now be visible.

### Manual Installation

Clone the repo:

    $ git clone https://github.com/tmux-plugins/tmux-battery ~/clone/path

Add this line to the bottom of `.tmux.conf`:

    run-shell ~/clone/path/battery.tmux

Reload TMUX environment:

    # type this in terminal
    $ tmux source-file ~/.tmux.conf

If format strings are added to `status-right`, they should now be visible.

### Changing icons

By default, these icons are displayed:

 - charged: ":battery:" ("❇ " when not on OS X)
 - charging: ":zap:"
 - discharging: (nothing shown)
 - attached but not charging: ":warning:"

You can change these defaults by adding the following to `.tmux.conf` (the
following lines are not in the code block so that emojis can be seen):

 - set -g @batt_charged_icon ":sunglasses:"
 - set -g @batt_charging_icon ":+1:"
 - set -g @batt_discharging_icon ":thumbsdown:"
 - set -g @batt_attached_icon ":neutral_face:"

Don't forget to reload tmux environment (`$ tmux source-file ~/.tmux.conf`)
after you do this.

### Range formatting

Three ranges for formatting are available:

 - Critical (default <10%, red)
 - Warning (default <30%, yellow)
 - OK (default >=30%, green)

These can be customised with a number of options, the first two set the limits:

 - set-option -g @batt_warn_thresh 30
 - set-option -g @batt_crit_thresh 10

The individual `#{battery_prefix}` and `#{battery_suffix}` format strings can
also be customised using the options:

 - set-option -g @batt_ok_prefix "[fg=green]"
 - set-option -g @batt_ok_suffix "[fg=default]"
 - set-option -g @batt_warn_prefix "[fg=yellow]"
 - set-option -g @batt_warn_suffix "[fg=default]"
 - set-option -g @batt_crit_prefix "[fg=red]"
 - set-option -g @batt_crit_suffix "[fg=default]"

An example using the [Powerline fonts](https://github.com/powerline/fonts) dividers:<br/>
![formatting](/screenshots/formatting.png)

### Limitations

- Battery icon change most likely won't be instant.<br/>
  When you un-plug power cord it will take some time (15 - 60 seconds) for the
  icon to change. This depends on the `status-interval` tmux option. Setting it
  to 15 seconds should be good enough.

### Other goodies

You might also find these useful:

- [resurrect](https://github.com/tmux-plugins/tmux-resurrect) - restore tmux
  environment after system restart
- [logging](https://github.com/tmux-plugins/tmux-logging) - easy logging and
  screen capturing
- [online status](https://github.com/tmux-plugins/tmux-online-status) - online status
  indicator in tmux `status-right`. Useful when on flaky connection to see if
  you're online.

You might want to follow [@brunosutic](https://twitter.com/brunosutic) on
twitter if you want to hear about new tmux plugins or feature updates.

### Contributors

- [@jgeralnik](https://github.com/jgeralnik)
- [@m1foley](https://github.com/m1foley)
- [@asethwright](https://github.com/asethwright)
- [@JanAhrens](https://github.com/JanAhrens)
- [@levens](https://github.com/levens)

### License

[MIT](LICENSE.md)
