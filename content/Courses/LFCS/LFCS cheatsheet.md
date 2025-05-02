# LFCS Command Cheat Sheet

## 🔧 System Information & Debugging

| Command                 | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| `sh -V`                 | Show version of the shell                                 |
| `hostnamectl`           | Change the static hostname of your Linux system           |
| `ssh -v alex@localhost` | Show verbose SSH connection messages to help debug issues |

## 📂 File & Directory Operations

| Command                  | Description                                                |
| ------------------------ | ---------------------------------------------------------- |
| `ls -la /home/bob/data/` | Find hidden files in a given directory                     |
| `touch /home/bob/myfile` | Create a file named `myfile` in the `/home/bob/` directory |

## 🔍 Manual & Search Utilities

| Command                | Description                      |
| ---------------------- | -------------------------------- |
| `apropos "NFS mounts"` | Search manual pages for keywords |

## 👤 User & Group Management

| Command                            | Description                                               |
| ---------------------------------- | --------------------------------------------------------- |
| `usermod -a -G developers jane`    | Add user `jane` to the `developers` group                 |
| `groupadd -g 9875 cricket`         | Create a group named `cricket` with GID 9875              |
| `groupmod -n soccer cricket`       | Rename `cricket` group to `soccer`                        |
| `useradd -G soccer sam --uid 5322` | Create user `sam` with UID 5322 and add to `soccer` group |
| `usermod -g rugby sam`             | Set primary group of `sam` to `rugby`                     |
| `usermod -L sam`                   | Lock user account `sam`                                   |
| `groupdel appdevs`                 | Delete the `appdevs` group                                |
| `chage -W 2 jane`                  | Warn `jane` 2 days before password expires                |
| `gpasswd -a trinity wheel`         | Add `trinity` to `wheel` group (sudo access)              |

## 💾 Mounting & Disk

| Command                                    | Description                              |
| ------------------------------------------ | ---------------------------------------- |
| `findmnt /dev/vda1`                        | Show mount options used with `/dev/vda1` |
| `umount /mnt`                              | Manually unmount file systems            |
| `mount -o ro,noexec,nosuid /dev/vdb1 /mnt` | Mount with specified options             |

## 🔐 SSL

| Command                                                       | Description                  |
| ------------------------------------------------------------- | ---------------------------- |
| `openssl req -newkey rsa:4096 -keyout priv.key -out cert.csr` | Generate private key and CSR |
| `openssl x509 -in my.crt -text`                               | Display certificate details  |

## 🧪 Git Operations

| Command                       | Description                            |
| ----------------------------- | -------------------------------------- |
| `git add *.cpp`               | Stage `.cpp` files for commit          |
| `git commit -m "Message"`     | Commit changes with a message          |
| `git branch testing`          | Create `testing` branch                |
| `git checkout master`         | Switch to `master` branch              |
| `git branch --delete testing` | Delete `testing` branch                |
| `git log --raw`               | Show raw commit log                    |
| `git merge "branch name"`     | Merge branch into current              |
| `git pull origin master`      | Pull latest changes from remote master |
| `git push origin master`      | Push commits to remote master          |
| `git clone "repository"`      | Clone remote repo                      |

## 🖥️ Operations & Scripts

| Command                             | Description                          |
| ----------------------------------- | ------------------------------------ |
| `shutdown +120`                     | Schedule shutdown after 120 minutes  |
| `grub-install /dev/vda`             | Install GRUB bootloader              |
| `systemctl get-default`             | Get system's default target          |
| `shutdown -c`                       | Cancel scheduled shutdown            |
| `./script.sh`                       | Run a script from current directory  |
| `chmod u+x ./script.sh`             | Make script executable               |
| `systemctl daemon-reload`           | Reload systemd manager configuration |
| `ps lax`                            | See detailed process info            |
| `sleep 10`                          | Pause for 10 seconds                 |
| `renice 9 <PID>`                    | Change priority of process           |
| `lsof -p 1`                         | List open files for PID 1            |
| `pgrep -a rpcbind`                  | Find PID of `rpcbind` process        |
| `kill -SIGHUP <pid>`                | Send `SIGHUP` to a process           |
| `grep -r --text 'reboot' /var/log/` | Recursively search logs for `reboot` |
| `ps u 1`                            | Show CPU & memory for PID 1          |
| `[command] &`                       | Run command in background            |

## ⏰ Scheduling

| Command         | Description                  |
| --------------- | ---------------------------- |
| `crontab -l`    | View root's crontab          |
| `anacron -n -f` | Force run all `anacron` jobs |
| `atq`           | List scheduled jobs          |
| `atrm <jobid>`  | Remove job by ID             |

## 📦 Package Management

| Command                                   | Description                       |                                  |
| ----------------------------------------- | --------------------------------- | -------------------------------- |
| `apt search "apache http server"`         | Search for Apache package         |                                  |
| `apt install apache2`                     | Install Apache web server         |                                  |
| `dpkg --search /bin/ls`                   | Find package owning a file        |                                  |
| \`dpkg --listfiles coreutils              | grep ^/bin\`                      | List `/bin` files in `coreutils` |
| `apt-get remove --auto-remove -y ziptool` | Remove `ziptool` and dependencies |                                  |

## 📊 System Monitoring

| Command        | Description             |
| -------------- | ----------------------- |
| `df /`         | Show disk usage of root |
| `du -sh /bin/` | Show size of `/bin/`    |
| `free --mega`  | Show memory in MB       |
| `uptime`       | Show system uptime      |
| `lscpu`        | Show CPU architecture   |

## 🧱 SELinux

| Command                                        | Description                         |
| ---------------------------------------------- | ----------------------------------- |
| `xfs_repair /dev/vdb`                          | Repair XFS filesystem               |
| `sysctl -w kernel.modules_disabled=1`          | Disable module loading              |
| `ls -Z /bin/sudo`                              | View SELinux label                  |
| `chcon -t httpd_sys_content_t /var/index.html` | Change SELinux context              |
| `setenforce 0`                                 | Set SELinux to permissive mode      |
| `semanage user -l`                             | List SELinux users and roles        |
| `restorecon -R /var/log/`                      | Restore SELinux context recursively |

## 🧑‍💻 More User & Shell Commands

| Command                       | Description                                   |
| ----------------------------- | --------------------------------------------- |
| `usermod -e 2030-03-01 jane`  | Expire `jane` on date                         |
| `usermod -e "" jane`          | Unexpire `jane`                               |
| `useradd -s /bin/csh -m jack` | Create user `jack` with csh shell             |
| `userdel -r jack`             | Delete `jack` and home dir                    |
| `chage --lastday 0 jane`      | Force `jane` to change password on next login |
| `nproc`                       | Show max allowed processes                    |
| `echo $MYVAR`                 | Print value of an env variable                |
| `env`                         | Print environment                             |
| `source ~/.bashrc`            | Reload shell config                           |
| `touch path/file`             | Create new file(s)                            |

## 🌐 Networking

| Command                                     | Description             |
| ------------------------------------------- | ----------------------- |
| `ss -tunlp`                                 | Show listening sockets  |
| `ip a`                                      | Show interfaces         |
| `ip route show`                             | Show routing table      |
| `ip a add 192.168.9.3/24 dev eth1`          | Add IP to interface     |
| `netplan apply`                             | Apply Netplan config    |
| `netstat -tulpn`                            | Show active connections |
| `timedatectl`                               | Show time settings      |
| `timedatectl set-timezone America/New_York` | Set timezone            |
| `ufw enable`                                | Enable firewall         |
| `ufw allow 22`                              | Allow SSH               |
| `ufw deny 443/tcp`                          | Deny HTTPS              |
| `ufw delete deny 443/tcp`                   | Remove deny rule        |
| `ufw status numbered`                       | List firewall rules     |
| `ufw allow from 207.45.232.181`             | Allow specific IP       |
| `ufw allow from 10.11.12.0/24`              | Allow subnet            |
| `ufw delete 8`                              | Delete rule #8          |

## 💽 Storage & LVM

| Command                                  | Description                  |
| ---------------------------------------- | ---------------------------- |
| `lsblk`                                  | List block devices           |
| `mkswap /dev/vdb3`                       | Format as swap               |
| `swapon --show`                          | Show active swap             |
| `fdisk /dev/vdb`                         | Partition disk               |
| `mkswap /dev/vdb2`                       | Create swap on vdb2          |
| `swapon /dev/vdb2`                       | Enable swap                  |
| `swapoff /dev/vdb2`                      | Disable swap                 |
| `cfdisk`                                 | Partition manager            |
| `mkfs.xfs -L "DataDisk" /dev/vdb`        | Create XFS FS with label     |
| `mkfs.ext4 -N 2048 /dev/vdc`             | Create ext4 with 2048 inodes |
| `mount /dev/vdb /mnt`                    | Mount device                 |
| `umount /mnt`                            | Unmount                      |
| `xfs_admin -L "SwapFS" /dev/vdb`         | Rename label                 |
| `exportfs -r`                            | Re-export NFS                |
| `pvcreate /dev/vdb /dev/vdc`             | Create PVs                   |
| `pvs`                                    | List PVs                     |
| `pvremove /dev/vdc`                      | Remove PV                    |
| `vgcreate volume1 /dev/vdb`              | Create VG                    |
| `vgextend volume1 /dev/vdc`              | Extend VG                    |
| `vgreduce volume1 /dev/vdc`              | Remove disk from VG          |
| `vgs`                                    | Show VGs                     |
| `lvcreate`                               | Create LV                    |
| `lvresize --size 752M volume1/smalldata` | Resize LV                    |
| `mkfs.xfs /dev/volume1/smalldata`        | Format LV                    |
| `lvremove volume1/smalldata`             | Delete LV                    |

## 📁 ACLs & Quotas

| Command                                                                | Description                     |
| ---------------------------------------------------------------------- | ------------------------------- |
| `getfacl archive`                                                      | List ACLs on `archive`          |
| `mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/vdb /dev/vdc` | Create RAID 1 array             |
| `setfacl --modify user:john:rw specialfile`                            | Give `john` RW on `specialfile` |
| `setfacl --remove user:john specialfile`                               | Remove `john`'s ACL             |
| `setfacl --modify group:mail:rx specialfile`                           | Give group `mail` RX access     |
| `setfacl --recursive --modify user:john:rwx collection/`               | Recursive ACL for `john`        |
| `xfs_quota -x -c 'limit bsoft=100m bhard=500m john' /dev/vda1`         | Set disk quota for `john`       |
