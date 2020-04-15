### commands manipulation
- copy output of previous command: cmd+shift+a, cmd+c

### file and folder/directory (used interchangebaly)
- create a folder: `mkdir folder_name`
- reach/access a directory:
  - a sub folder under the current folder: `cd sub-directory-name`
  - a specific folder: `cd path/to/destination/folder`
- copy a file to another folder: `cp file-name path/to/destination/folder`
- check file size within a folder: `ls -lh`

### system information
- check server time zone: `timedatectl`
- check all available time zones: `timedatectl list-timezones (| grep America)`
- change time zone: `sudo timedatectl set-timezone America/Los_Angeles`

### ssh commands
- access remote server: `ssh -i path/to/keypair.pem user@remote.com`
- copy file to remote server: `scp -i path/to/keypair.pem file user@remote.com:destination`

### vim editor
- create a text file: `$ vim new_file.txt`
- edit text file: `i`
- exit or quit editing mode: `esc`
- exit or quit file:`:q`
- save and quit editing mode: `wq`

### disk information
- check disk usage:
  - `$ df -hT /dev/nvme0n1p1`
- check disk file system: `sudo file -s /dev/nvme0n1p1`
