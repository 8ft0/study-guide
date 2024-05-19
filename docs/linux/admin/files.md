### Linux File Permissions Cheat Sheet

**Purpose**: To provide a quick reference for understanding and managing file permissions in Linux.

---

#### Understanding File Permissions

1. **Permission Types**:
   - **r**: Read - allows reading the file or listing the directory.
   - **w**: Write - allows modifying the file or directory.
   - **x**: Execute - allows executing the file or entering the directory.

2. **Permission Groups**:
   - **User (u)**: The owner of the file.
   - **Group (g)**: Users who are members of the file's group.
   - **Others (o)**: All other users.

3. **Permission Structure**:
   - Displayed using `ls -l`:
     ```sh
     -rwxr-xr--
     ```
   - Breakdown:
     - **-**: File type (e.g., `-` for a regular file, `d` for a directory).
     - **rwx**: User permissions.
     - **r-x**: Group permissions.
     - **r--**: Other permissions.

#### Viewing Permissions

1. **List File Permissions**:
   ```sh
   ls -l <filename>
   ```

2. **List Directory Permissions**:
   ```sh
   ls -ld <directory>
   ```

#### Changing Permissions

1. **Using Symbolic Notation**:
   - **Add permission**:
     ```sh
     chmod u+x <filename>  # Add execute permission to the user
     chmod g+w <filename>  # Add write permission to the group
     chmod o+r <filename>  # Add read permission to others
     ```
   - **Remove permission**:
     ```sh
     chmod u-x <filename>  # Remove execute permission from the user
     chmod g-w <filename>  # Remove write permission from the group
     chmod o-r <filename>  # Remove read permission from others
     ```
   - **Set exact permission**:
     ```sh
     chmod u=rwx,g=rx,o=r <filename>
     ```

2. **Using Numeric Notation**:
   - Permissions are represented by a three-digit octal number.
     - **r = 4**, **w = 2**, **x = 1**.
     - Combine values to set permissions (e.g., `rwx = 4+2+1 = 7`).

   - **Set permissions**:
     ```sh
     chmod 755 <filename>  # User: rwx, Group: rx, Others: r
     chmod 644 <filename>  # User: rw, Group: r, Others: r
     ```

#### Changing Ownership

1. **Change File Owner**:
   ```sh
   chown <new-owner> <filename>
   ```

2. **Change File Group**:
   ```sh
   chown :<new-group> <filename>
   ```

3. **Change Owner and Group**:
   ```sh
   chown <new-owner>:<new-group> <filename>
   ```

4. **Recursive Ownership Change**:
   ```sh
   chown -R <new-owner>:<new-group> <directory>
   ```

#### Special Permissions

1. **Setuid (Set User ID)**:
   - Execute file as the owner, not as the user who runs it.
   ```sh
   chmod u+s <filename>
   ```

2. **Setgid (Set Group ID)**:
   - New files in the directory inherit the group of the directory.
   ```sh
   chmod g+s <directory>
   ```

3. **Sticky Bit**:
   - Only the file owner can delete files in the directory.
   ```sh
   chmod +t <directory>
   ```

#### Viewing and Setting Special Permissions

1. **Viewing Special Permissions**:
   ```sh
   ls -l <filename>  # Look for 's' (setuid/setgid) or 't' (sticky bit)
   ```

2. **Setting Special Permissions** (Numeric Notation):
   - **Setuid**: 4
   - **Setgid**: 2
   - **Sticky Bit**: 1
   ```sh
   chmod 4755 <filename>  # Setuid
   chmod 2755 <directory>  # Setgid
   chmod 1755 <directory>  # Sticky bit
   ```

By using this cheat sheet, new starters can effectively manage and understand file permissions in Linux, ensuring proper access control and security.