Linux File Permissions:

---

**Question:** 

You are given the following line from the output of the `ls -l` command in Linux:

```
-rw-r--r-- 1 user group 1024 May 16 12:34 example.txt
```

Based on this information, answer the following questions:

### Q1: What are the permissions of the file `example.txt`?

A. Read and write for the owner, read for the group and others.

B. Read, write, and execute for the owner, read for the group and others.

C. Read, write, and execute for the owner, group, and others.

D. Read and write for the owner, read and execute for the group and others.

### Q2: What command would you use to change the permissions of `example.txt` to `-rwxr-xr--`?

A. `chmod 755 example.txt`

B. `chmod 744 example.txt`

C. `chmod 764 example.txt`

D. `chmod 754 example.txt`

### Q3: What does the `1` in the output `-rw-r--r-- 1 user group 1024 May 16 12:34 example.txt` represent?

A. The number of hard links to the file.

B. The file size in bytes.

C. The number of users who have access to the file.

D. The inode number of the file.

### Q4: If you want to give the group write permissions to the file `example.txt`, which command would you use?

A. `chmod g+w example.txt`

B. `chmod g-w example.txt`

C. `chmod o+w example.txt`

D. `chmod o-w example.txt`

### Q5: What is the effect of the following command: `chmod 600 example.txt`?

A. Sets read and write permissions for the owner only.

B. Sets read and write permissions for the owner and group.

C. Sets read, write, and execute permissions for the owner only.

D. Sets read, write, and execute permissions for the owner and group.

---

### Answers:

1. A. Read and write for the owner, read for the group and others.
2. A. `chmod 755 example.txt`
3. A. The number of hard links to the file.
4. A. `chmod g+w example.txt`
5. A. Sets read and write permissions for the owner only.

---

### Answers:

**Q1: What are the permissions of the file `example.txt`?**

- **Answer: A. Read and write for the owner, read for the group and others.**

- Explanation: The permissions `-rw-r--r--` indicate that the owner has read and write permissions, while the group and others have read permissions only.

**Q2: What command would you use to change the permissions of `example.txt` to `-rwxr-xr--`?**

- **Answer: D. `chmod 754 example.txt`**

- Explanation: The permissions `-rwxr-xr--` correspond to the numerical value `754`. The owner has read, write, and execute permissions (`7`), the group has read and execute permissions (`5`), and others have read permissions (`4`).

**Q3: What does the `1` in the output `-rw-r--r-- 1 user group 1024 May 16 12:34 example.txt` represent?**

- **Answer: A. The number of hard links to the file.**

- Explanation: The `1` in the output indicates the number of hard links to the file.

**Q4: If you want to give the group write permissions to the file `example.txt`, which command would you use?**

- **Answer: A. `chmod g+w example.txt`**

- Explanation: The command `chmod g+w example.txt` adds write permissions for the group.

**Q5: What is the effect of the following command: `chmod 600 example.txt`?**

- **Answer: A. Sets read and write permissions for the owner only.**

- Explanation: The permissions `600` mean that the owner has read and write permissions (`6`), while the group and others have no permissions (`0` each).

---

