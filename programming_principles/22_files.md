# 23. Files

### 23.01. An overview of file and directories in Windows, Linux and Mac OS

The file system is one of the most important portions of an operating system. Today there are different OSs (Operating Systems) existing in the computer science world, but the most common known are three: Windows (Microsoft), Mac OS (Apple) and Ubuntu (Linux/UNIX system, free and open source). But what is a file system? What is a file? What is a directory? We're going to answer all these questions (and others) in this chapter.

A file system is the way an operating system organizes and manages data on storage devices (like HD -Hard Disk-, flash memory, or SSD -Solid State Disk-) and it defines how files are stored, named, and accessed. NTFS, FAT32 and ext4 are three examples of common file systems.

A file is a named collection of data stored on disk, normally seen as a byte stream. Each file stored in a storage device can have zero, one, or more bytes and it can contain text, images, code, or binary data. A file is stored in a specific directory of the file system and, from the logical point-of-view, it has the own name (called filename also) and the own extensions. For example, a Python source code is a file with the `.py` extension. An extension indicates some info about the file content.

A directory (folder) is a container used to organize files and other directories and it's a part of the file system. It helps structure data in a hierarchical way, and each directory contains files and subdirectories. The structure of a file system, independently of the OS installed in the system, is organized in a hierarchy: in Linux and Mac OS there is only one root directory, meanwhile Windows can have one, two, or more root directory (in function of the partition of the storage devices).

A path is a string that specifies the location of a file or directory in a file system: each path is unique into the same file system. Two files with the same filename cannot exist into the same directory. A path is a logical way to tell to the OS where a file, a directory, or a subdirectory is located in the storage devices. There are two types of path:

- An absolute path specifies the location of file, directory, or subdirectory from the root of the file system. It includes the complete path to traverse the entire file system from the root, up to the affected node.
- A relative path specifies the location of file, directory, or subdirectory from the current working directory. The current working directory is an information associated to the current user. For example, if you open a shell in the `/myprograms` directory, your current working directory is exactly `/myprograms`. You can specify a path relative to your current working directory.

In Windows, an example of an absolute path is:

```bash
C:\Users\Alice\Documents\file.txt
```

In Linux, or Mac OS X, an example of absolute path is:

```bash
/home/bob/file.txt
```

Windows is case-insensitive, Linux and Mac OS X are case-sensitive. It means that the two files `file.txt` and `FILE.txt` are the same in Windows, but they're considered different in Linux and Mac OS X. For all operating system, in relative paths, `.` is the current directory and `..` is the parent directory. 

### 23.02. File modes and file opening with `open()`
<!-- to do -->

### 23.03. File reading with `read()`, `readline()` and `readlines()`
<!-- to do -->

### 23.04. File writing with `write()` and `writelines`
<!-- to do -->

### 23.05. File closing with `close()`
<!-- to do -->

### 23.06. Context managers with the `with` keyword
<!-- to do -->

### 23.07. Text and binary files
<!-- to do -->

### 23.08. Sequential and random access with `seek()` and `tell()`
<!-- to do -->

### 23.09. Temporary files
<!-- to do -->

### 23.10. File Permissions
<!-- to do -->

### 23.11. JSON Files
<!-- to do -->

### 23.12. CSV Files
<!-- to do -->

### 23.13. Serialization and Deserialization
<!-- to do -->

### 23.14. Files with `pickle`
<!-- to do -->

### 23.15. Files with `shelve`
<!-- to do -->
