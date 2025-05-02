# Things I Didn't Know

- `journalctl` is a command to read system logs.
- `Pager` a viewer in Linux.
- `man man` Gives list of available parameters when querying manuals.
- `apropos` A command to help find information in man.
  - The first attempt of using apropos may fail if the database is not created yet.
  - run `sudo mandb`
  - This typically is only required if the command is run very early in the linux servers life.
  - Can provide tag `-s` and give a list of sections we are interested in. (E.G Command are found in sections 1 and 8).
- `ls` parameter `-l` shows output in long format, including permissions. `-a` shows all files including hidden ones. `-h` shows file sizes.
- `cd -` returns you to your previous directory.
- `cp [source] [destination]`
  - `-r` is or recursive copying.
- `stat [file]` shows information regarding a file including:
  - size, block, access, modify, change, birth.
  - Inode keeps track of pieces of memory and metadata.
- `find [dir] -perm /[permission]` Returns files and directories with
  the specified permissions.
  - `find . -perm /4000` returns executables with SUID set.
