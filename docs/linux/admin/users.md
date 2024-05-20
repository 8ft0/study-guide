### Linux User Configuration Cheat Sheet

**Purpose**: To provide a quick reference for managing user accounts and groups on a Linux system.

---

#### Creating and Managing Users

1. **Create a New User**:
      ```sh
      sudo useradd <username>
      ```
      - With home directory creation:
      ```sh
      sudo useradd -m <username>
      ```
      - With a specific shell:
      ```sh
      sudo useradd -s /bin/bash <username>
      ```
      - With a specific home directory:
      ```sh
      sudo useradd -m -d /home/<username> <username>
      ```

2. **Set User Password**:
   ```sh
   sudo passwd <username>
   ```

3. **Modify User Account**:
      - Change user's shell:
      ```sh
      sudo usermod -s /bin/zsh <username>
      ```
      - Change user's home directory:
      ```sh
      sudo usermod -d /new/home/directory <username>
      ```
      - Lock user account:
      ```sh
      sudo usermod -L <username>
      ```
      - Unlock user account:
      ```sh
      sudo usermod -U <username>
      ```

4. **Delete a User**:
      ```sh
      sudo userdel <username>
      ```
      - Delete user along with home directory and mail spool:
      ```sh
      sudo userdel -r <username>
      ```

#### Managing Groups

1. **Create a New Group**:
   ```sh
   sudo groupadd <groupname>
   ```

2. **Add User to Group**:
   ```sh
   sudo usermod -aG <groupname> <username>
   ```

3. **Remove User from Group**:
   ```sh
   sudo gpasswd -d <username> <groupname>
   ```

4. **Change User's Primary Group**:
   ```sh
   sudo usermod -g <groupname> <username>
   ```

5. **Delete a Group**:
   ```sh
   sudo groupdel <groupname>
   ```

#### Viewing User and Group Information

1. **List All Users**:
   ```sh
   cut -d: -f1 /etc/passwd
   ```

2. **View User Information**:
   ```sh
   id <username>
   ```
   - Detailed user information:
     ```sh
     getent passwd <username>
     ```

3. **List All Groups**:
   ```sh
   cut -d: -f1 /etc/group
   ```

4. **View Group Information**:
   ```sh
   getent group <groupname>
   ```

#### User and Group Configuration Files

1. **/etc/passwd**:
      - Contains user account information.
      - Format: `username:x:UID:GID:comment:home_directory:shell`
      - Example entry:
      ```sh
      jan:x:1001:1001:Jan:/home/jan:/bin/bash
      ```

2. **/etc/shadow**:
      - Contains secure user account information.
      - Format: `username:password:last_change:min:max:warn:inactive:expire:flag`
      - Example entry:
      ```sh
      jan:$6$saltsaltsaltsalt$hashedpassword:18449:0:99999:7:::
      ```

3. **/etc/group**:
      - Contains group account information.
      - Format: `groupname:x:GID:member1,member2,member3`
      - Example entry:
      ```sh
      sudo:x:27:jan
      ```

#### Common Tasks

1. **Switch User**:
   ```sh
   su - <username>
   ```

2. **Execute Command as Another User**:
   ```sh
   sudo -u <username> <command>
   ```

3. **Display Logged-in Users**:
   ```sh
   who
   ```

4. **Show User's Last Login**:
   ```sh
   lastlog -u <username>
   ```

By using this cheat sheet, new starters can efficiently manage user and group configurations on a Linux system, ensuring proper account setup and maintenance.