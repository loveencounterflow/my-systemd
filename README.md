
# My SystemD Timers

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [My SystemD Timers](#my-systemd-timers)
  - [Symlink Timers In Home Folder](#symlink-timers-in-home-folder)
  - [Tools](#tools)
    - [Install SystemD UI, GUI](#install-systemd-ui-gui)
    - [Cockpit](#cockpit)
  - [Command Lines](#command-lines)
  - [See Also](#see-also)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->



# My SystemD Timers

## Symlink Timers In Home Folder

"$USER"

## Tools

### Install SystemD UI, GUI

https://askubuntu.com/a/1124446/1597241

> If you are using amd64 system, you can download the packages **systemd-ui_3-4_amd64.deb** and **systemd-gui_3-4_all.deb** from Xenial Repository and manually install with apt:
>
>     sudo apt install ./systemd-ui_3-4_amd64.deb
>     sudo apt install ./systemd-gui_3-4_all.deb
>
> I did this and worked like a charm.
>
>     systemadm
>
> Bibliography:
>
> * [https://launchpad.net/ubuntu/+source/systemd-ui][1]
> * [https://launchpad.net/ubuntu/+archive/primary/+files/systemd-gui_3-4_all.deb][2]
> * [https://launchpad.net/ubuntu/+archive/primary/+files/systemd-ui_3-4_amd64.deb][3]
>
>
>   [1]: https://launchpad.net/ubuntu/+source/systemd-ui
>   [2]: https://launchpad.net/ubuntu/+archive/primary/+files/systemd-gui_3-4_all.deb
>   [3]: https://launchpad.net/ubuntu/+archive/primary/+files/systemd-ui_3-4_amd64.deb

```bash
sudo apt install ~/Downloads/systemd-ui_3-4_amd64.deb
sudo apt install ~/Downloads/systemd-gui_3-4_all.deb
```

(works but is spartanic and likes to freeze whenever SystemD is reloaded so maybe not worth it)

### Cockpit

https://cockpit-project.org/running.html

under consideration


## Command Lines

```bash
sudo systemctl daemon-reload                                && \
  systemctl --user reset-failed flow-timed-beeper.service   && \
  systemctl --user reset-failed flow-timed-beeper.timer     && \
  systemctl --user enable flow-timed-beeper.service         && \
  systemctl --user enable flow-timed-beeper.timer           && \
  systemctl --user start flow-timed-beeper.timer
```

Test service (once):

```bash
systemctl --user start flow-timed-beeper.service
```

```bash
systemctl list-timers
systemctl --user --all list-timers
```

```bash
systemctl --user list-unit-files
```

<!--

play /usr/share/mint-artwork/sounds/notification.oga
which play

man systemd.time
l /etc/systemd/system/
#
systemctl status flow-timed-beeper.timer
journalctl -xe
journalctl -p 5 -xb


sudo systemctl daemon-reload && systemctl --user enable flow-timed-beeper.timer && systemctl --user start flow-timed-beeper.timer

 -->


## See Also

* [Restart
  Limits](https://serverfault.com/questions/845471/service-start-request-repeated-too-quickly-refusing-to-start-limit)
* `wiki.ubuntuusers.de`
  * [*Service Units*](https://wiki.ubuntuusers.de/systemd/Service_Units/)
    * [*systemd Service Unit Beispiel*](https://wiki.ubuntuusers.de/Howto/systemd_Service_Unit_Beispiel/)
  * [*Timer Units*](https://wiki.ubuntuusers.de/systemd/Service_Units/)
* [*Scheduling tasks with systemd timers on
  Linux*](https://www.fosslinux.com/48317/scheduling-tasks-systemd-timers-linux.htm) (uses `--user` option
  in contradistinction to many other accounts that claim you have to use `sudo`, install files in
  `/etc/systemd`)
