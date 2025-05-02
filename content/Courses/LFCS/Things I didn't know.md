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

## File Systems

### Hard Links

A hard link is an additional entry in the file system that points to the same inode as the original file. (\_Inode keeps track of pieces of memory and metadata.)

An example of using hard links, some user x stores an image at `/home/a/image.jpg` if user x wanted to share the image with user y then, instead of copying the image into `/home/y/image.jpg` doubling the required storage, a link can be made to the current path file.

```bash
ln /home/x/image.jpeg /home/y/image.jpeg
```

If the x deletes his hard link this does not remove the hard link of user y. When there is zero hard links the data is deleted from the file system.

You can only hard link to files not directories.
You can only hard link to the files on the same filesystem.

Make sure you proper permissions to create link at the destination. Referring to the above example you would need write permissions at `/home/y/`.

Make sure all users have the required permissions, for example add users to the same group and then add read and write permissions for that file for that group.

### Soft Links

Soft links are files that point to a path.

`ln -s [path to target] [path to link]` ensure symbolic/.soft link.

Using the same hard link example above:

```bash
ln -s /home/x/image.jpeg image_shortcut_.jpeg
```

Running `ls -l` where this soft link is created would output something like:

```bash
lrwxrwxrwx. 1 x x image_shortcut.jpeg -> /home/x/image.jpeg
```

`readlink [file]` will output the path to the actual file/directories.

Soft links work for different file systems.

## File Permissions

Any file or directory is owned by a user. Only the owner of a file ro directory can change the permissions. The only exception is root.

using `ls -l` we can highlight the user and group:

```bash
-rw-r-----. 1 [user] [group] 49 Oct 27 14:41 example.pdf
```

- `chgrp [group_name] [file/directory]` changes the group of the the file.
- `groups` list all the groups
- `chown [user]:[group] [file/dir]` changes the owner and/or group (only root user can change user need to use sudo.)

Focussing on the first section of the `ls -l` output:

The first character indicates the type:

| File Type        | Identifier |
| :--------------- | :--------: |
| directory        |     d      |
| regular file     |     -      |
| character device |     c      |
| link             |     l      |
| socket file      |     s      |
| pipe             |     p      |
| block device     |     b      |

Following the file type specification the permissions are defined. Here I have used square brackets to delineate between owner, group and other respectively, `[rwx][rwx][rwx]`. Provided is a table defining what each letter corresponds to in permissions.

| Bit | Purpose       |
| :-: | :------------ |
|  r  | Read file     |
|  w  | Write to file |
|  x  | Execute (run) |
|  -  | No permission |

Permissions work linearly, as owner, group and others. The permissions terminates at any of those. For example if a file `test.txt` has owner `x` and group `g` with the following permissions `-r--rw-r--`. If user `x` tries to write to `test.txt` it will be denied. Even though they are part of the group. However if Jane is part of the group but is not an owner she will have write permissions.

To change permissions you can use the command: `chmod [permissions] [file/directory]`

| Class         | Option  | Examples (where `*` = `+,-,=`) |
| ------------- | :-----: | ------------------------------ |
| <u>u</u>ser   | u +/-/= | `u * w`/ `u * rw` / `u * rwx`  |
| <u>g</u>roup  | g +/-/= | `g * w` / `g * rw` / `g * rwx` |
| <u>o</u>thers | o +/-/= | `o * w` / `o * rw` / `o * rwx` |
