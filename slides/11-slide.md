# INTERACTIVE SHELL

![Slide11](https://i.postimg.cc/w6x38T39/slides11.jpg)

```
$ python3 -c 'import pty; pty.spawn(â/bin/bashâ)'
â CTRL+Z
$ stty raw -echo; fg
â ENTER, ENTER
$ echo $TERM
dumb
$ stty size
67 318
$ export TERM=xterm-256color
$ export stty rows 67 columns 318
```

## [NEXT SLIDE  - PRIV ESC | ROOT USER ðð½](12-slide.md)
