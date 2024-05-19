## Challenge Name: File Metadata Organisation

### Description:
You are given a directory containing various types of files (text files, images, scripts, etc.). Your task is to write a shell script that organises these files based on their file types into subdirectories named after the file type. Additionally, generate a summary report detailing the number of files for each file type.

### Requirements:
1. **Organise files by type**:
   - Move files into subdirectories based on their file extensions.
   - Create a subdirectory for each file type (e.g., `txt`, `jpg`, `sh`).
   - If a subdirectory for a file type already exists, just move the file into it.

2. **Generate summary report**:
   - Count the number of files for each file type.
   - Output the summary report to a file named `file_summary.txt`.

### Input:
- A directory named `files` containing various types of files.

### Output:
- Organised subdirectories inside the `files` directory.
- A summary report in a file named `file_summary.txt` with the following format:
  ```
  File Summary Report
  ===================
  txt: <number of txt files>
  jpg: <number of jpg files>
  sh: <number of sh files>
  ...
  ```

### Example:
Suppose the `files` directory contains the following files:
- `document1.txt`
- `document2.txt`
- `image1.jpg`
- `script1.sh`
- `script2.sh`
- `image2.jpg`

After running the script, the `files` directory should have the following structure:
```
files/
  ├── txt/
  │   ├── document1.txt
  │   └── document2.txt
  ├── jpg/
  │   ├── image1.jpg
  │   └── image2.jpg
  ├── sh/
  │   ├── script1.sh
  │   └── script2.sh
```

And `file_summary.txt` should contain:
```
File Summary Report
===================
txt: 2
jpg: 2
sh: 2
```

### Constraints:
- Your script should be written in bash.
- Assume the `files` directory always contains valid files with proper extensions.
- Your script should handle an arbitrary number of files in the `files` directory.

### Submission:
Submit your bash script file with the name `organise_files.sh`.

## Solution:

Here is a possible solution in the form of a bash script:

```bash
#!/bin/bash

# Check if the files directory exists
if [ ! -d "files" ]; then
  echo "Directory 'files' not found!"
  exit 1
fi

# Initialize an associative array to hold the count of each file type
declare -A file_count

# Process each file in the files directory
for file in files/*; do
  if [ -f "$file" ]; then
    # Get the file extension
    extension="${file##*.}"
    
    # Create a subdirectory for the file type if it doesn't exist
    if [ ! -d "files/$extension" ]; then
      mkdir "files/$extension"
    fi

    # Move the file to the corresponding subdirectory
    mv "$file" "files/$extension/"

    # Increment the file type count
    ((file_count[$extension]++))
  fi
done

# Generate file summary report
summary_file="files/file_summary.txt"
echo "File Summary Report" > "$summary_file"
echo "===================" >> "$summary_file"
for ext in "${!file_count[@]}"; do
  echo "$ext: ${file_count[$ext]}" >> "$summary_file"
done

echo "Files have been organised and summary report generated at $summary_file"
```

### Explanation:

1. **Check if the files directory exists**: The script ensures that the `files` directory is present before proceeding.

2. **Initialise an associative array for file counts**: The script sets up an associative array `file_count` to keep track of the number of files for each extension.

3. **Process each file**: The script iterates through each file in the `files` directory, extracts the file extension, creates a corresponding subdirectory if it doesn't exist, moves the file into the subdirectory, and updates the file count.

4. **Generate the summary report**: The script creates a `file_summary.txt` file in the `files` directory, writes the counts of each file type, and prints a completion message.

This solution assumes the `files` directory contains valid files with proper extensions and is named correctly. Adjustments may be needed based on specific requirements or variations in input.