In C, file handling functions like `fopen()`, `fread()`, `fwrite()`, and `fseek()` are used to work with files. Here's a simple explanation for each:

### 1. **`fopen()`**
- **Purpose:** Opens a file to either read, write, or append data.
- **Usage:** 
  ```c
  FILE *file = fopen("filename.txt", "mode");
  ```
- **Parameters:**
  - `"filename.txt"`: The name of the file to open.
  - `"mode"`: How the file should be opened:
    - `"r"`: Read-only. File must exist.
    - `"w"`: Write. Creates a new file or overwrites an existing file.
    - `"a"`: Append. Adds data to the end of the file.
- **Returns:** A pointer to a `FILE` object or `NULL` if it fails.

---

### 2. **`fread()`**
- **Purpose:** Reads binary data from a file into memory.
- **Usage:**
  ```c
  size_t result = fread(buffer, size, count, file);
  ```
- **Parameters:**
  - `buffer`: Memory location where data is stored.
  - `size`: Size of each element to read (in bytes).
  - `count`: Number of elements to read.
  - `file`: Pointer to the opened file (`FILE *`).
- **Returns:** Number of elements successfully read.

---

### 3. **`fwrite()`**
- **Purpose:** Writes binary data from memory to a file.
- **Usage:**
  ```c
  size_t result = fwrite(buffer, size, count, file);
  ```
- **Parameters:**
  - `buffer`: Memory location containing data to write.
  - `size`: Size of each element to write (in bytes).
  - `count`: Number of elements to write.
  - `file`: Pointer to the opened file (`FILE *`).
- **Returns:** Number of elements successfully written.

---

### 4. **`fseek()`**
- **Purpose:** Moves the file position indicator to a specific location in the file.
- **Usage:**
  ```c
  int status = fseek(file, offset, origin);
  ```
- **Parameters:**
  - `file`: Pointer to the opened file (`FILE *`).
  - `offset`: Number of bytes to move.
  - `origin`: Starting point:
    - `SEEK_SET`: Beginning of the file.
    - `SEEK_CUR`: Current position in the file.
    - `SEEK_END`: End of the file.
- **Returns:** `0` on success, or a non-zero value on failure.

---

### Example Program:
```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.bin", "wb"); // Open file for writing
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    int data[] = {1, 2, 3, 4, 5};
    fwrite(data, sizeof(int), 5, file); // Write array to file
    fclose(file); // Close file

    file = fopen("example.bin", "rb"); // Reopen for reading
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    int buffer[5];
    fread(buffer, sizeof(int), 5, file); // Read data into buffer
    for (int i = 0; i < 5; i++) {
        printf("%d ", buffer[i]);
    }
    fclose(file); // Close file
    return 0;
}
```

This program writes an array to a binary file and reads it back. Functions like `fseek()` can be used to navigate through the file for more advanced operations.
