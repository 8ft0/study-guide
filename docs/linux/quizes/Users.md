Linux User Configuration:

---

**Question:**

You are tasked with configuring user accounts on a Linux system. Based on your knowledge of Linux user configuration files and commands, answer the following questions:

### Q1: Which command is used to add a new user on a Linux system?

A. `useradd`

B. `adduser`

C. `newuser`

D. `createuser`

### Q2: What file contains user account information such as username, user ID (UID), and home directory?

A. `/etc/group`

B. `/etc/shadow`

C. `/etc/passwd`

D. `/etc/login.defs`

### Q3: Which command can be used to change a user's password?

A. `passwd`

B. `chpasswd`

C. `usermod`

D. `chage`

### Q4: Where are user passwords stored in a hashed format on most Linux systems?

A. `/etc/passwd`

B. `/etc/shadow`

C. `/etc/security/passwd`

D. `/etc/user`

### Q5: What is the purpose of the `/etc/skel` directory?

A. To store user passwords in a secure manner.

B. To contain default files and directories that are copied to a new user's home directory when the user is created.

C. To store system-wide configuration files.

D. To contain the list of users with administrative privileges.

---

### Answers:

**Q1: Which command is used to add a new user on a Linux system?**

- **Answer: A. `useradd`**

- Explanation: The `useradd` command is used to create a new user account on a Linux system.

**Q2: What file contains user account information such as username, user ID (UID), and home directory?**

- **Answer: C. `/etc/passwd`**

- Explanation: The `/etc/passwd` file contains information about user accounts, including the username, UID, and home directory.

**Q3: Which command can be used to change a user's password?**

- **Answer: A. `passwd`**

- Explanation: The `passwd` command is used to change a user's password.

**Q4: Where are user passwords stored in a hashed format on most Linux systems?**

- **Answer: B. `/etc/shadow`**

- Explanation: The `/etc/shadow` file contains user passwords in a hashed format for security purposes.

**Q5: What is the purpose of the `/etc/skel` directory?**

- **Answer: B. To contain default files and directories that are copied to a new user's home directory when the user is created.**

- Explanation: The `/etc/skel` directory holds default configuration files and directories that are copied to the home directory of new users when their accounts are created.

---

