# Log-Archival-Automation-Script

A simple Bash script that archives log directories into compressed `.tar.gz` files. The script also provides options to delete the original logs after archiving and can transfer the archive to a remote server using SCP.

## Features

* Compresses a log directory into a `.tar.gz` archive.
* Creates archive filenames with the current date and time.
* Option to:

  * Archive only.
  * Archive and delete the original log directory.
* Supports transferring the archive to a remote Linux server via SCP.

## Prerequisites

Before running the script, ensure you have:

* Linux
* Bash
* `tar`
* `scp`
* Appropriate permissions to read the log directory
* `sudo` privileges if choosing to delete the directory

## Project Structure

```
.
├── log_archive.sh
└── README.md
```

## Usage

Make the script executable:

```bash
chmod +x log_archive.sh
```

Run the script by providing the log directory as an argument:

```bash
./log_archive.sh /path/to/log_directory
```

Example:

```bash
./log_archive.sh /var/log
```

## How It Works

### Step 1: Archive Option

The script asks whether you want to keep or delete the original log directory after archiving.

```
For archive and delete enter 1
For archive only enter 2
```

* **1** → Compresses the directory and deletes the original.
* **2** → Compresses the directory while keeping the original.

The generated archive follows this naming format:

```
log_archive_YYYYMMDD_HHMMSS.tar.gz
```

Example:

```
log_archive_20260702_153045.tar.gz
```

---

### Step 2: Archive Transfer

After creating the archive, the script asks where to send it.

```
For sending the archived folder to a remote server enter 1
```

#### Remote Server

If you choose **1**, you will be prompted for:

* Username
* Server IP address
* Destination directory

The archive is then transferred using `scp`.

Example:

```bash
scp log_archive_20260702_153045.tar.gz user@192.168.1.100:/home/user/backups/
```

## Example

```bash
$ ./log_archive.sh /var/log

For archive and delete enter 1, For archive only enter 2: 2

Archiving had been done successfully

For sending the archived folder to a remote server enter 1: 1

Enter the user name: ubuntu

Enter the server IP: 192.168.1.100

Enter the path of the destination directory: /home/ubuntu/backups
```

## Technologies Used

* Bash
* Tar
* SCP
* Linux Shell

