### Linux Backup and Recovery Study Sheet

**Purpose**: To provide a quick reference for performing backup and recovery tasks on a Linux system.

---

#### Backup Basics

1. **Types of Backups**:
      - **Full Backup**: A complete copy of all data.
      - **Incremental Backup**: Copies only the data that has changed since the last backup.
      - **Differential Backup**: Copies all data that has changed since the last full backup.

2. **Common Backup Tools**:
      - `rsync`: Synchronize files and directories.
      - `tar`: Archive files.
      - `dd`: Low-level copying and conversion.
      - `rsnapshot`: Filesystem snapshot utility.
      - `Bacula`, `Amanda`: Enterprise-level backup solutions.
      - `Timeshift`: System restore utility.

#### `rsync` for Backups

1. **Basic rsync Command**:
      ```sh
      rsync -avh /source/directory /destination/directory
      ```
      - `-a`: Archive mode (preserves permissions, timestamps, etc.).
      - `-v`: Verbose output.
      - `-h`: Human-readable output.

2. **Using `rsync` Over SSH**:
   ```sh
   rsync -avh -e ssh /source/directory user@remote:/destination/directory
   ```

3. **Incremental Backup with `rsync`**:
   ```sh
   rsync -avh --link-dest=/previous/backup /source/directory /destination/directory
   ```

#### `tar` for Backups

1. **Creating a tar Archive**:
      ```sh
      tar -cvzf backup.tar.gz /directory/to/backup
      ```
      - `-c`: Create a new archive.
      - `-v`: Verbose output.
      - `-z`: Compress the archive with gzip.
      - `-f`: Specify the filename.

2. **Extracting a tar Archive**:
      ```sh
      tar -xvzf backup.tar.gz -C /path/to/restore
      ```
      - `-x`: Extract files from an archive.
      - `-C`: Specify the directory to extract files to.

3. **Incremental Backup with `tar`**:
      - Create a full backup:
      ```sh
      tar -cvzf full-backup.tar.gz /directory/to/backup
      ```
      - Create an incremental backup:
      ```sh
      tar -cvzf incremental-backup.tar.gz --listed-incremental=/path/to/snapshot.file /directory/to/backup
      ```

#### `dd` for Backups

1. **Creating a Disk Image**:
      ```sh
      dd if=/dev/sdX of=/path/to/backup.img bs=4M
      ```
      - `if`: Input file (source device).
      - `of`: Output file (destination image file).
      - `bs`: Block size (default is 512 bytes, `4M` for 4 MB blocks).

2. **Restoring a Disk Image**:
   ```sh
   dd if=/path/to/backup.img of=/dev/sdX bs=4M
   ```

#### `rsnapshot` for Backups

1. **Install rsnapshot**:
   ```sh
   sudo apt install rsnapshot  # Debian/Ubuntu
   sudo yum install rsnapshot  # Red Hat/CentOS
   ```

2. **Configure rsnapshot**:
      - Edit the configuration file `/etc/rsnapshot.conf`.
      - Define backup intervals (hourly, daily, weekly, etc.).
      - Example configuration snippet:
      ```conf
      snapshot_root   /path/to/snapshots/
      backup  /home/  localhost/
      backup  /etc/   localhost/
      ```

3. **Run rsnapshot Backup**:
   ```sh
   sudo rsnapshot hourly
   sudo rsnapshot daily
   sudo rsnapshot weekly
   ```

#### `Timeshift` for System Restore

1. **Install Timeshift**:
   ```sh
   sudo apt install timeshift  # Debian/Ubuntu
   sudo dnf install timeshift  # Fedora
   ```

2. **Configure Timeshift**:
      - Launch Timeshift GUI:
      ```sh
      sudo timeshift
      ```
      - Select the snapshot type (RSYNC/BTRFS) and configure settings.

3. **Create and Restore Snapshots**:
      - Create a snapshot:
      ```sh
      sudo timeshift --create --comments "Manual backup"
      ```
      - Restore a snapshot:
      ```sh
      sudo timeshift --restore
      ```

#### Backup Automation with Cron

1. **Schedule a Backup Job**:
      - Edit the crontab file:
      ```sh
      crontab -e
      ```
      - Add a cron job (example: daily backup at 2 AM):
      ```sh
      0 2 * * * /usr/bin/rsync -avh /source/directory /destination/directory
      ```

#### Best Practices for Backup and Recovery

1. **Regular Backups**: Schedule regular backups to minimize data loss.
2. **Offsite Backups**: Store backups in a different physical location.
3. **Encryption**: Encrypt sensitive data backups for security.
4. **Testing**: Regularly test backup and recovery processes to ensure reliability.
5. **Documentation**: Document backup and recovery procedures for easy reference.

By using this study sheet, new starters can effectively manage backup and recovery tasks on a Linux system, ensuring data integrity and availability.