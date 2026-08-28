# Linux Cheat Sheet

## System Information

```bash
uname -a
hostname
hostnamectl
uptime

whoami
id
who
w

cat /etc/os-release
```

## Filesystem Navigation

```bash
pwd
ls
ls -la
ls -lah

cd /path/to/directory
cd ..
cd ~
cd -
```

## File Operations

```bash
touch file
mkdir directory
mkdir -p path/to/directory

cp file destination
cp -r directory destination

mv file destination

rm file
rm -r directory
rm -rf directory
```

Identify files:

```bash
file file
stat file
```

## Finding Files

```bash
find / -name "filename" 2>/dev/null
find / -type f 2>/dev/null
find / -type d 2>/dev/null

find /var -type f -name "*.log" 2>/dev/null
find /home -type f -user username 2>/dev/null
```

## Reading Files

```bash
cat file
less file
head file
tail file
tail -f logfile
```

## Searching Text

```bash
grep "pattern" file
grep -i "pattern" file
grep -n "pattern" file
grep -r "pattern" directory/
grep -v "pattern" file
```

## Permissions

```bash
ls -l

chmod 644 file
chmod 755 file
chmod +x script.sh

chown user file
chown user:group file
```

Permission values:

```text
r = read      4
w = write     2
x = execute   1

755 = rwxr-xr-x
644 = rw-r--r--
700 = rwx------
600 = rw-------
```

## Users and Groups

```bash
whoami
id
groups
groups username

who
w

cat /etc/passwd
cat /etc/group
```

Check sudo privileges:

```bash
sudo -l
```

## Processes

```bash
ps
ps aux
top
htop

pgrep process
pidof process

kill PID
kill -TERM PID
kill -KILL PID

pkill process
```

## Services

```bash
systemctl status service
systemctl start service
systemctl stop service
systemctl restart service

systemctl enable service
systemctl disable service

systemctl list-units --type=service
```

## Logs

```bash
journalctl
journalctl -f
journalctl -b
journalctl -u service
journalctl --since "1 hour ago"

dmesg
```

Common locations:

```text
/var/log/
/var/log/auth.log
/var/log/syslog
/var/log/messages
```

## Networking

```bash
ip addr
ip link
ip route
ip neigh

ss -tuln
ss -tunap

ping <host>
traceroute <host>

dig <domain>
nslookup <domain>

curl <url>
wget <url>
```

## SSH

```bash
ssh user@host
ssh -p 2222 user@host

scp file user@host:/path/
scp user@host:/path/file .
```

## Package Management

### Debian / Ubuntu

```bash
sudo apt update
sudo apt install <package>
sudo apt remove <package>
sudo apt upgrade

apt search <package>
apt show <package>
```

### Arch Linux

```bash
sudo pacman -Syu
sudo pacman -S <package>
sudo pacman -R <package>

pacman -Ss <package>
pacman -Qi <package>
```

## Archives

```bash
tar -cf archive.tar files/
tar -xf archive.tar

tar -czf archive.tar.gz files/
tar -xzf archive.tar.gz

zip archive.zip file
unzip archive.zip
```

## Disk Usage

```bash
df -h
du -sh directory/
du -h --max-depth=1
lsblk
mount
```

## Environment Variables

```bash
env
printenv
echo $PATH
echo $HOME
echo $USER

export VARIABLE=value
```

## Cron

List current user's scheduled jobs:

```bash
crontab -l
```

Edit them:

```bash
crontab -e
```

System-wide cron locations:

```text
/etc/crontab
/etc/cron.d/
/etc/cron.hourly/
/etc/cron.daily/
/etc/cron.weekly/
/etc/cron.monthly/
```

## Shell History

```bash
history
history | grep command

!!              # Repeat previous command
!123            # Execute history entry
```

## Useful Shortcuts

```text
Ctrl+C      Stop process
Ctrl+Z      Suspend process
Ctrl+D      Exit shell
Ctrl+L      Clear terminal
Ctrl+A      Beginning of line
Ctrl+E      End of line
Ctrl+R      Search history
Tab         Autocomplete
```
