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

Python has a built-in function for file opening, called `open()`. When you want to use a file in a Python code, first you must open it with the `open()` built-in function. Open a file means the Python runtime prepares the I/O stream to read and/or write the file. Remember that a file is simply a group of sequential bytes.

But now let's analyze the `open()` built-in function. `open()` accepts two parameters:

- The `filename` (or a relative/absolute path containing the filename).
- The `mode`, which is the type of the I/O operation and the way that Python uses to access and write the file.

The `mode` is particularly important cause it determines how the file is written, or read. Moreover, the `mode` parameter tells to the Pyton interpreter how the file must be interpreted (as a text file, or binary file). All the following are possible values for the `mode` parameter:

- `r`: it opens the file in read mode and it's the default value for the `mode` parameter. If the file doesn't exist, Python will throw an error.
- `w`: it opens the file in write mode. It creates the file if it doesn't exist. `w` overwrites the current content of the file.
- `a`: it opens the file in append mode. It means that the file already exists, the new content is appened (written after the current content of the file). It creates the file if it doesn't exist. `a` doesn't overwrite the current content of the file.
- `x`: it oepns the file in create mode. If the file already exists, Python will throw an error.

You can add the `t` letter to specify a text file (default value), or the `b` letter to specify a binary file. We'll talk about these two modes in the next paragraphs.

You can use the `open()` built-in function in this way:

```python
f = open("file.txt")
```

The previous line of code opens a file in the current working directory called `file.txt` in read mode (`r` is the default) and text mode (`t` is the default). `f` is a variable containing the file object. Python allows the developer to read and write a file only through its file object. The previous line is equivalent of the following:

```python
f = open("file.txt", "rt")
```

### 23.03. File reading with `read()`, `readline()` and `readlines()`

We consider a file called `text.txt` with the following simple content:

```txt
Hello! Welcome to text.txt
This file is for testing purposes.
Good Luck!
```

So, the file object returned from the `open()` function has three main function to read a file:

- `read()` reads the entire contents of the files (all lines). It returns a string. It can take a size argument to read a specific number of characters.
- `readline()` reads a single line of the file. If you call `readline()` more times, it returns different lines (strings): first, secondo and so on. The new line character (represented by `\n`) is included in the string. This method is very useful if you want to iterate the file content line-by-line.
- `readlines()` reads all lines at once and it returns a list of string in which each string is a line of the file. Each string includes the `\n` chacrater at the end. If you want a list of string, this method is perfect.

Let's start using the read methods of the object file! The following code prints in the standard output the entire content of the `text.txt` file:

```python
f = open("text.txt")
print(f.read()) # Hello! Welcome to text.txt
                # This file is for testing purposes.
                # Good Luck!
```

In the following example, we print line-by-line:

```python
f = open("text.txt")
print(f.readline()) # Hello! Welcome to text.txt
print(f.readline()) # This file is for testing purposes.
print(f.readline()) # Good Luck!
```

We've called the `readline()` method three times and we've printed each line separately.

Here's an example of using `readlines()` with the `for` loop:

```python
f = open("text.txt")
for line in f.readlines():
    print(line)     # Hello! Welcome to text.txt
                    # This file is for testing purposes.
                    # Good Luck!
```

### 23.04. File writing with `write()` and `writelines()`

A file object has both `write()` and `writelines()` methods. To open a file in writing mode, you can use both `w` and `a` letters as `mode` parameter of the `open()` built-in function. `w` re-write the entire file, from the start and the previous content is lost; `a` starts the writing from the end of the file, so the previous content isn't lost.

`write()` can write one, or more lines as you want (it depends by the `\n` character):

```python
f = open("text.txt", "w")
f.write("This is the first line\n") # 23
f.write("This is the second line\n") # 24
```

When you use the `write()` method, you must specify the `\n` character (it isn't isnerted automatically). So, what is the integer number returned by the `write()` method? It's the number of character successfully written to the file, if you've opened the file in text mode (`t`); if you writing the file in binary mode, it's the number of bytes successfully written to the file.

The `writelines()` method accepts a list of string: tipically, each element of the list (or iterable) is a line if you include the `\n` character. Here's an example:

```python
f = open("text.txt", "w")
f.writelines([
    "This is the first line\n",
    "This is the second line\n",
    "This is the third line\n"
])
```

Differently from the `write()` method, `writelines()` doesn't return any value.

### 23.05. File closing with `close()`

If you want to close the file you're using (in reading, or writing mode), you can use the `close()` method:

```python
f = open("text.txt")

# ... some code to read/write the file ...

f.close()
```

It's very important to always close the file, if all operations about it are terminated. This action optimizes the file system resources provided by the operating system.

### 23.06. Context managers with the `with` keyword

You can use a context manager to read/write a file by using the `with` keyword provided by the Python programming language. Here's an example:

```python
with open("text.txt") as f:
    for line in f:
        print(line)
```

Note that we used the `for` loop to iterate over the file content by writing the expression `line in f`: Python sees a file object as an iterable you can iterate over when you reading it.

Use a context manager has some advantages:

- First of all, at the end of the `with` code, the file is automatically close. You don't need to specify the `f.close()` statement.
- Second, it's recommended in PEP 343.
- Third, you need to write less code to handle the file opening and the file closing.
- Fourth, it's a clearer code: you can immediately understand the purpose of it.
- Fifth, it ensures proper cleanup on exceptions.

To summarize, using the `with` keyword ensures files are automatically and safely closed, making code cleaner and more reliable.

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
