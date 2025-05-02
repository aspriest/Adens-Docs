# File Systems

## Hard Links

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

## Soft Links

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

Alternatively, you can use number codes to set the permissions. The number are calculated by splitting `rwxrwxrwx` into three binary parts and then merging the result decimal values together. I ave provided a table indicating the binary dn decimal relations.

| Binary | Decimal |
| :----: | :-----: |
|  000   |    0    |
|  001   |    1    |
|  010   |    2    |
|  011   |    3    |
|  100   |    4    |
|  101   |    5    |
|  110   |    6    |
|  111   |    7    |

Example command: `chmod 777 [file/directory]`

## SUID, SGID and Sticky Bit

### SUID

A special permission that allows users to run an executable with the permissions of the executable's owner.

When using SUID we can use the `chmod` command. Now when running chmod we include an additional digit at the beginning. For SUID that is `4`.

e.g.

```bash
chmod 4664 example-file
```

Looking at the output of such a command there is two states of interest:

`-rwSrw-r--` or `-rwsrw-r--`

- `S` indicates that the user has executable write by SUID but not by permissions.
- `s` indicates that the user has both executable write by SUID and permissions.

### SGID

A similar permission, but applies to both executables and directories.

When using SGID we can use the `chmod` command. Now when running chmod we include an additional digit at the beginning. For SUID that is `2`.

e.g.

```bash
chmod 4664 example-file
```

Looking at the output of such a command there is two states of interest:

`-rw-rwSr--` or `-rw-rwsr--`

- `S` indicates that the user has executable write by SGID but not by permissions.
- `s` indicates that the user has both executable write by SGID and permissions.

### Sticky Bit

A special permission that can be set on directories. It restricts file deletion in that directory.

`chmod +t [directory]` or `chmod 1777 [directory]` are example sof how to set a sticky bit. Noting that the `777` is an arbitrary permissions number.
