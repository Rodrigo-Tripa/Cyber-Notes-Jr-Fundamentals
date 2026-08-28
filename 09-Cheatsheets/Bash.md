# Bash Cheat Sheet

## Navigation

```bash
pwd                         # Print working directory
ls                          # List directory contents
ls -la                      # List all files, including hidden files
ls -lh                      # Human-readable file sizes
cd /path/to/directory       # Change directory
cd ..                       # Move to parent directory
cd ~                        # Move to home directory
cd -                         # Return to previous directory
```

## Files and Directories

```bash
touch file.txt              # Create an empty file
mkdir directory             # Create a directory
mkdir -p a/b/c              # Create nested directories

cp file.txt /tmp/           # Copy a file
cp -r directory/ /tmp/      # Copy a directory
mv old.txt new.txt          # Move or rename
rm file.txt                 # Remove a file
rm -r directory/            # Remove a directory recursively

file file.txt               # Identify file type
stat file.txt               # Display file metadata
```

## Reading Files

```bash
cat file.txt                # Display file contents
less file.txt               # Read interactively
head file.txt               # First 10 lines
head -n 20 file.txt         # First 20 lines
tail file.txt               # Last 10 lines
tail -n 20 file.txt         # Last 20 lines
tail -f logfile.log         # Follow a changing file
nl file.txt                 # Display numbered lines
```

## Searching

```bash
find /path -name "file.txt"
find /path -type f
find /path -type d
find /path -type f -name "*.log"

grep "pattern" file.txt
grep -i "pattern" file.txt
grep -n "pattern" file.txt
grep -r "pattern" directory/
grep -v "pattern" file.txt
```

Combine commands when searching is required:

```bash
ps aux | grep "process"
cat file.txt | grep "password"
find /var/log -type f | grep ".log"
```

## Pipes

A pipe (`|`) sends the standard output of one command to the standard input of another.

```bash
command1 | command2
command1 | grep "text"
cat file.txt | sort | uniq
ps aux | grep ssh
```

## Redirection

```bash
command > file.txt          # Overwrite file
command >> file.txt         # Append to file
command < file.txt          # Read input from file
command 2> error.log        # Redirect stderr
command > out 2>&1          # Redirect stdout and stderr
command &> output.log       # Redirect stdout and stderr
```

## Command Chaining

```bash
command1 ; command2         # Execute both commands
command1 && command2        # Execute second if first succeeds
command1 || command2        # Execute second if first fails
command &                   # Run in background
```

## Text Processing

```bash
sort file.txt               # Sort lines
uniq file.txt               # Remove adjacent duplicates
sort file.txt | uniq        # Sort and deduplicate
wc -l file.txt              # Count lines
wc -w file.txt              # Count words
cut -d ':' -f 1 file.txt    # Extract field
tr 'a-z' 'A-Z'              # Transform characters
sed 's/old/new/g' file.txt  # Replace text
awk '{print $1}' file.txt   # Print first field
```

## Permissions

```bash
ls -l file
chmod 644 file
chmod 755 file
chmod +x script.sh
chown user file
chown user:group file
```

Permission values:

```text
r = 4
w = 2
x = 1

7 = rwx
6 = rw-
5 = r-x
4 = r--
0 = ---
```

## Processes

```bash
ps
ps aux
top
htop

pgrep process
kill PID
kill -9 PID
pkill process

jobs
fg
bg
```

## Environment

```bash
whoami
id
hostname
uname -a

env
echo $PATH
echo $HOME

export VAR=value
```

## Archives

```bash
tar -cf archive.tar files/
tar -xf archive.tar

tar -czf archive.tar.gz files/
tar -xzf archive.tar.gz

zip archive.zip file.txt
unzip archive.zip
```

## Help

```bash
man command
command --help
help command

which command
type command
```

## History

```bash
history
history | grep command

!!                          # Repeat previous command
!123                        # Execute history entry 123
```

## Useful Shortcuts

```text
Ctrl+C      Terminate current command
Ctrl+Z      Suspend current command
Ctrl+D      Exit shell / end input
Ctrl+L      Clear terminal
Ctrl+A      Beginning of line
Ctrl+E      End of line
Ctrl+U      Delete before cursor
Ctrl+K      Delete after cursor
Ctrl+R      Search command history
Tab         Autocomplete
```
