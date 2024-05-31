### Coreutils Study Sheet

**Purpose**: To provide a quick reference for using GNU Core Utilities (coreutils) on a Linux system, covering basic file, text, and system commands.

---

#### File Operations

1. **List Files**:
      - Basic listing:
      ```sh
      ls
      ```
      - Detailed listing:
      ```sh
      ls -l
      ```
      - Include hidden files:
      ```sh
      ls -a
      ```

2. **Copy Files**:
      - Basic copy:
      ```sh
      cp <source> <destination>
      ```
      - Copy directories recursively:
      ```sh
      cp -r <source-dir> <destination-dir>
      ```

3. **Move/Rename Files**:
   ```sh
   mv <source> <destination>
   ```

4. **Remove Files**:
      - Basic remove:
      ```sh
      rm <file>
      ```
      - Remove directories recursively:
      ```sh
      rm -r <directory>
      ```
      - Force remove:
      ```sh
      rm -f <file>
      ```

5. **Create Directories**:
      ```sh
      mkdir <directory>
      ```
      - Create parent directories as needed:
      ```sh
      mkdir -p <parent/child-directory>
      ```

6. **Remove Directories**:
   ```sh
   rmdir <directory>
   ```

7. **Change File Permissions**:
      ```sh
      chmod <permissions> <file>
      ```
      - Example to make a file executable:
      ```sh
      chmod +x <file>
      ```

8. **Change File Ownership**:
   ```sh
   chown <owner>:<group> <file>
   ```

9. **Link Files**:
      - Create a hard link:
      ```sh
      ln <target> <link-name>
      ```
      - Create a symbolic link:
      ```sh
      ln -s <target> <link-name>
      ```

#### Text Operations

1. **Display File Contents**:
      - Basic display:
      ```sh
      cat <file>
      ```
      - Display with line numbers:
      ```sh
      cat -n <file>
      ```

2. **Concatenate Files**:
   ```sh
   cat <file1> <file2> > <output-file>
   ```

3. **View File with Paging**:
      ```sh
      less <file>
      ```
      - Alternative command:
      ```sh
      more <file>
      ```

4. **Search Inside Files**:
      ```sh
      grep <pattern> <file>
      ```
      - Recursive search:
      ```sh
      grep -r <pattern> <directory>
      ```

5. **Count Lines, Words, Characters**:
      ```sh
      wc <file>
      ```
      - Count lines only:
      ```sh
      wc -l <file>
      ```

6. **Sort Lines**:
   ```sh
   sort <file>
   ```

7. **Remove Duplicate Lines**:
   ```sh
   uniq <file>
   ```

8. **Compare Files**:
   ```sh
   diff <file1> <file2>
   ```

9. **Replace Text in Files**:
      - Basic replace:
      ```sh
      sed 's/<old>/<new>/g' <file>
      ```
      - Replace and save changes:
      ```sh
      sed -i 's/<old>/<new>/g' <file>
      ```

#### System Operations

1. **Print Working Directory**:
   ```sh
   pwd
   ```

2. **Change Directory**:
   ```sh
   cd <directory>
   ```

3. **Display Disk Usage**:
      - Disk space usage of files and directories:
      ```sh
      du -sh <directory>
      ```
      - Disk free space:
      ```sh
      df -h
      ```

4. **Display Process Information**:
      - List all processes:
      ```sh
      ps aux
      ```
      - Filter processes by name:
      ```sh
      ps aux | grep <process-name>
      ```

5. **Terminate a Process**:
      ```sh
      kill <PID>
      ```
      - Force terminate:
      ```sh
      kill -9 <PID>
      ```

6. **System Uptime**:
   ```sh
   uptime
   ```

7. **Display System Information**:
   ```sh
   uname -a
   ```

8. **Change File Timestamps**:
   ```sh
   touch <file>
   ```

#### Archiving and Compression

1. **Create Archive**:
   ```sh
   tar -cvf <archive-name>.tar <file-or-directory>
   ```

2. **Extract Archive**:
   ```sh
   tar -xvf <archive-name>.tar
   ```

3. **Create Compressed Archive**:
   ```sh
   tar -czvf <archive-name>.tar.gz <file-or-directory>
   ```

4. **Extract Compressed Archive**:
   ```sh
   tar -xzvf <archive-name>.tar.gz
   ```

By using this study sheet, new starters can efficiently perform common file, text, and system operations on a Linux system, leveraging the powerful utilities provided by coreutils.