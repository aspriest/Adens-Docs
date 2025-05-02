# Things I Didn't Know

- `journalctl` is a command to read system logs.
-  `Pager` a viewer in Linux.
- ``` man man ``` Gives list of available parameters when querying manuals.
- `apropos` A command to help find information in man.
    - The first attempt of using apropos may fail if the database is not created yet. 
    - run `sudo mandb`
    - This typically is only required if the command is run very earlt in the linux servers life.
    - Can provide tag `-s` and give a list of sections we are interested in. (E.G Command are found in sections 1 and 8).