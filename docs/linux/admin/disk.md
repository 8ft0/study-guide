### Linux Disk Management Cheat Sheet

**Purpose**: To provide a quick reference for managing disks and filesystems on a Linux system.

---

#### Viewing Disk Information

1. **View Disk Partitions**:
   ```sh
   lsblk
   ```
   - Alternative command:
     ```sh
     fdisk -l
     ```

2. **View Disk Usage**:
   ```sh
   df -h
   ```

3. **View Inode Usage**:
   ```sh
   df -i
   ```

4. **View Block Device Attributes**:
   ```sh
   lsblk -f
   ```

5. **View Filesystem Type**:
   ```sh
   blkid
   ```

#### Partitioning Disks

1. **Using `fdisk`**:
   - Open `fdisk` for a specific disk:
     ```sh
     sudo fdisk /dev/sdX
     ```
   - Common `fdisk` commands:
     - `n`: Add a new partition
     - `d`: Delete a partition
     - `p`: Print the partition table
     - `w`: Write changes and exit

2. **Using `parted`**:
   - Open `parted` for a specific disk:
     ```sh
     sudo parted /dev/sdX
     ```
   - Common `parted` commands:
     - `print`: Display the partition table
     - `mklabel gpt`: Create a new GPT partition table
     - `mkpart primary ext4 0% 100%`: Create a primary partition spanning the entire disk
     - `quit`: Exit `parted`

#### Creating Filesystems

1. **Create an ext4 Filesystem**:
   ```sh
   sudo mkfs.ext4 /dev/sdX1
   ```

2. **Create an XFS Filesystem**:
   ```sh
   sudo mkfs.xfs /dev/sdX1
   ```

3. **Create a Btrfs Filesystem**:
   ```sh
   sudo mkfs.btrfs /dev/sdX1
   ```

4. **Create a Swap Partition**:
   ```sh
   sudo mkswap /dev/sdX2
   sudo swapon /dev/sdX2
   ```

#### Mounting and Unmounting Filesystems

1. **Mount a Filesystem**:
   ```sh
   sudo mount /dev/sdX1 /mnt
   ```

2. **Unmount a Filesystem**:
   ```sh
   sudo umount /mnt
   ```

3. **View Mounted Filesystems**:
   ```sh
   mount | column -t
   ```

4. **Mount a Filesystem at Boot**:
   - Edit `/etc/fstab`:
     ```sh
     sudo nano /etc/fstab
     ```
   - Add an entry:
     ```sh
     /dev/sdX1 /mnt ext4 defaults 0 2
     ```

#### Resizing Partitions and Filesystems

1. **Resize an ext4 Filesystem**:
   - **Increase**:
     ```sh
     sudo resize2fs /dev/sdX1
     ```
   - **Decrease** (unmount first):
     ```sh
     sudo umount /dev/sdX1
     sudo resize2fs /dev/sdX1 <size>
     sudo mount /dev/sdX1
     ```

2. **Resize an XFS Filesystem**:
   - **Increase**:
     ```sh
     sudo xfs_growfs /mnt
     ```
   - **Decrease**: XFS does not support shrinking.

3. **Resize a Partition** (using `parted`):
   - Open `parted`:
     ```sh
     sudo parted /dev/sdX
     ```
   - Resize partition:
     ```sh
     resizepart PARTITION_NUMBER END
     ```
   - Adjust the filesystem size as necessary.

#### Managing LVM (Logical Volume Manager)

1. **Create Physical Volume**:
   ```sh
   sudo pvcreate /dev/sdX1
   ```

2. **Create Volume Group**:
   ```sh
   sudo vgcreate my_vg /dev/sdX1
   ```

3. **Create Logical Volume**:
   ```sh
   sudo lvcreate -L 10G -n my_lv my_vg
   ```

4. **Extend Logical Volume**:
   ```sh
   sudo lvextend -L +5G /dev/my_vg/my_lv
   sudo resize2fs /dev/my_vg/my_lv
   ```

5. **Reduce Logical Volume**:
   - Unmount the filesystem first:
     ```sh
     sudo umount /dev/my_vg/my_lv
     sudo resize2fs /dev/my_vg/my_lv <new_size>
     sudo lvreduce -L <new_size> /dev/my_vg/my_lv
     sudo mount /dev/my_vg/my_lv
     ```

6. **Remove Logical Volume**:
   ```sh
   sudo lvremove /dev/my_vg/my_lv
   ```

7. **Remove Volume Group**:
   ```sh
   sudo vgremove my_vg
   ```

8. **Remove Physical Volume**:
   ```sh
   sudo pvremove /dev/sdX1
   ```

By using this cheat sheet, new starters can effectively manage disks and filesystems on a Linux system, ensuring proper storage configuration and maintenance.