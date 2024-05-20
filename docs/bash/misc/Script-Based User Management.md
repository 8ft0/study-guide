# Script-Based User Management

### Description:
You are tasked with creating a shell script that performs user management operations on a Linux system. The script should be able to add a new user, delete an existing user, and list all users on the system. Each operation should be specified by a command-line argument.

### Requirements:
1. **Add a new user**: The script should accept a username as an argument and create a new user with that name.
2. **Delete an existing user**: The script should accept a username as an argument and delete the user with that name.
3. **List all users**: The script should list all users currently on the system.

### Input:
- Command-line arguments specifying the operation (`add`, `delete`, `list`) and the username (for `add` and `delete` operations).

### Output:
- Appropriate messages indicating the success or failure of each operation.

### Example:
- To add a new user:
  ```
  ./user_management.sh add newuser
  ```
  Output:
  ```
  User 'newuser' added successfully.
  ```
- To delete an existing user:
  ```
  ./user_management.sh delete newuser
  ```
  Output:
  ```
  User 'newuser' deleted successfully.
  ```
- To list all users:
  ```
  ./user_management.sh list
  ```
  Output:
  ```
  List of users:
  user1
  user2
  ...
  ```

### Constraints:
- Your script should be written in bash.
- Ensure proper error handling for operations (e.g., user already exists, user does not exist).

### Submission:
Submit your bash script file with the name `user_management.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Function to add a new user
add_user() {
  username=$1
  if id "$username" &>/dev/null; then
    echo "Error: User '$username' already exists."
  else
    sudo useradd "$username"
    if [ $? -eq 0 ]; then
      echo "User '$username' added successfully."
    else
      echo "Error: Failed to add user '$username'."
    fi
  fi
}

# Function to delete an existing user
delete_user() {
  username=$1
  if id "$username" &>/dev/null; then
    sudo userdel "$username"
    if [ $? -eq 0 ]; then
      echo "User '$username' deleted successfully."
    else
      echo "Error: Failed to delete user '$username'."
    fi
  else
    echo "Error: User '$username' does not exist."
  fi
}

# Function to list all users
list_users() {
  echo "List of users:"
  cut -d: -f1 /etc/passwd
}

# Main script logic
if [ $# -lt 1 ]; then
  echo "Usage: $0 {add|delete|list} [username]"
  exit 1
fi

operation=$1
username=$2

case $operation in
  add)
    if [ -z "$username" ]; then
      echo "Error: No username specified for 'add' operation."
      exit 1
    fi
    add_user "$username"
    ;;
  delete)
    if [ -z "$username" ]; then
      echo "Error: No username specified for 'delete' operation."
      exit 1
    fi
    delete_user "$username"
    ;;
  list)
    list_users
    ;;
  *)
    echo "Error: Invalid operation specified. Use 'add', 'delete', or 'list'."
    exit 1
    ;;
esac
```

### Explanation:

1. **Add a new user**: The `add_user` function checks if the user already exists using the `id` command. If the user does not exist, it uses `useradd` to create the user and checks for success.

2. **Delete an existing user**: The `delete_user` function checks if the user exists using the `id` command. If the user exists, it uses `userdel` to delete the user and checks for success.

3. **List all users**: The `list_users` function lists all users by reading `/etc/passwd` and extracting the usernames.

4. **Main script logic**: The script processes command-line arguments to determine the operation (`add`, `delete`, `list`) and calls the appropriate function. It also includes error handling for missing arguments and invalid operations.

This script assumes it is run with appropriate permissions to manage users (typically as root or with `sudo`). Adjustments may be needed based on specific requirements or system configurations.