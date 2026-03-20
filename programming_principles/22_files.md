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

A file sotred in a specific path of the file system of a system can be of two types:

- Text file: a text file is seen as a characters stream. Each element of the stream is a character, compatible with the character set and text encoding used in the current system.
- Binary file: a binary file is seen as a bytes stream. Each element of the stream is a byte, which is a group of 8 bits (in numeric terms, it can be from 0 to 255, 256 possible values in total).

Both types of file are used in Python and which type of file to use depends on the application and the purposes you're implement in Python. These are the main differences between text and binary files:

- Content. A text file is a stream of character. A binary file is a stream of bytes.
- Readable. A text file is a human-readable file. A binary file is a stream of raw bytes (not human-readable).
- Encoding. A text file uses a specific encoding, or character set to represent each character. A binary file is seen as a bytes flow: it not use any encoding, or other.
- Mode. In Python, you can read/write a text file with `r`, or `w` modes. In Python, you can read/write a binary file with `rb`, or `wb` modes.
- Data Type. In Python, the content of a text file is a string (`str` data type). In Python, the content of a binary file is an array of bytes (`bytes` data type).

Examples of text file are: `.txt`, `.csv` and `.py`. Examples of binary files are: `.mp3`, `.mp4` and `.png`.

### 23.08. Sequential and random access with `seek()` and `tell()`

When you open a file to read, or write it, there is a pointer (called current position pointer) to track the last read you've made with `read()`, `readline()`, `readlines()`, `write()`, or `writelines()`. The file object has two useful method to manage the current position pointer: `seek()` and `tell()`.

The `tell()` method returns the current position of the file pointer, as an integer, representing the number of bytes from start. For example, if you write ten characters by using the ASCII encoding (each character is 1 byte, or 8 bits), `tell()` returns the value `10`, cause the next write starts from the 10th byte of the file. For example, the following code opens a file called `text.txt` in write mode and it writes two characters of one byte, so it calls the `tell()` method:

```python
f = open("text.txt", "w")
f.write("A\n")
print(f.tell()) # 2
```

If we try to write other two character of one byte, this happens:

```python
f.write("B\n")
print(f.tell()) # 4
```

The same topic for file reading:

```python
f = open("text.txt")

print(f.tell()) # 0
print(f.readline()) # "A"

print(f.tell()) # 2
print(f.readline()) # "B"

print(f.tell()) # 4
```

If you try to call a third time the `readline()` method, it returns an empty result and `f.tell()` always returns `4`, the end of the file (or told in another way, the number of bytes stored in the `text.txt` file).

`seek()` is the complementary method of `tell()`, cause it has the main prupose to locate the current pointer location. The `seek()` method accepts two parameters:

- `offset`: is the number of bytes from the start of the file. It's an integer and it's a required parameter.
- `whence`: indicates how the offset is related to the current position. There are three pissibility:
    - `0`: it's the default value and it indicates the offset is referred at the beginning of the file.
    - `1`: the offset is referred to the current position of the file.
    - `2`: the offset is referred to the end of the file.

Here's an example:

```python
f = open("text.txt")

print(f.tell()) # 0
print(f.readline()) # A

f.seek(0) # equivalent to f.seek(0, 0), or f.seek(0, whence = 0)
print(f.readline()) # A
print(f.tell()) # 2

f.seek(0) # equivalent to f.seek(0, 0), or f.seek(0, whence = 0)
print(f.readline()) # A
print(f.tell()) # 2
```

You can position the pointer at the end of the file with this line of code:

```python
f.seek(0, whence = 2)
```

or:

```python
f.seek(0, 2)
```

### 23.09. Temporary files

Python has a library called `tempfile` to use the temporary file. Temporary files are files created to store data temporarily during program execution and they're usually used to store data useful for the program (caching, debugging, or testing). A temporary file tipically is created when the program starts its execution and it's deleted when the program ends its execution.

To use a temporary file, in Python, you must import the `tempfile` module:

```python
import tempfile
```

You can use `tempfile.TemporaryFile()` to create a new temporary file completely and automatically handled by the `tempfile` module. To use `tempfile.TemporaryFile()`, you should use the context manager (the `with` keyword):

```python
with tempfile.TemporaryFile() as tf:
    tf.write(b"Hello")
    tf.seek(0)
    print(tf.read()) # "Hello"
```

In the previous example, `tempfile` module creates a new temporary file and, thanks to the context manager, we rename it as `tf`. Into the context manager block, we've three statements: the first statement writes `"Hello"` string in the file as a bytes flow; the second statement change the pointer of the file to the start (byte `0`); the third reads the content of the written temporary file.

You can use `tempfile.NamedTemporaryFile()`, a temporary file that has a name stored in the `name` property of the file:

```python
with tempfile.NamedTemporaryFile() as tf:
    print(tf.name)
```

You can also create a temporary directory with `tempfile.TemporaryDirectory()`:

```python
with tempfile.TemporaryDirectory() as td:
    print(td)
```

Remember that, thanks to a context manager, all resources (files and directories) are cleanup automatically when the context manager block ends.

### 23.10. JSON Files
<!-- to do -->

### 23.11. CSV Files
<!-- to do -->

### 23.12. Serialization and Deserialization of data structures and objects
<!-- to do -->

### 23.13. Files with `pickle`

`pickle` is a module used to serialize (save) and deserialize (load) Python objects. It converts objects into a byte stream that can be stored in a file, for this reason `pickle` is used  to save complex data structures (like lists, dicts and objects).

The action of object saving is called pickling. In the following code, first we import the `pickle` module by the `import pickle` statement. Second, we create a dict with the keys `"name"` and `"age"`. Finally, we use a context manager to create a binary file called `data.pkl` (note the extension of pickle files: `.pkl`).


```python
import pickle

data = {"name": "Alice", "age": 30}

with open("data.pkl", "wb") as f:
    pickle.dump(data, f) # pickling
```

The function provided by the `pickle` module is `pickle.dump()`: it accepts the complex data structure to serialize (in our case, a dict) as first positional parameter and the pickle file where the data must be serialized as second positional parameter (in our case, the file called `data.pkl`, referred by the `f` identifier). Note that we used the `open()` built-in function with the `wb` mode: in Python, a complex data structure is always saved as a bytes stream.

The action of object loading is called unpickling. The code is very similar to the previous, but we use the `pickle.load()` function to load the serialized data in a specific file into a Python variable:

```python
import pickle

with open("data.pkl", "rb") as f:
    data = pickle.load(f) # unpickling
    print(data)
```

Note that we used the `open()` built-in function with the `rb` mode: in Python, a complex data structure is always loaded as a bytes stream.

### 23.14. Files with `shelve`

`shelve` is a module that provides a persistent, dictionary-like object stored on the storage memory. You can access it with keys and values just like a normal dict, but the content is saved between program runs. Under the hood, `shelve` uses `pickle`, so keys must be strings and values must be pickleable Python objects. A shelve database usually creates one or more files depending on the platform and backend.

The recommended way to work with a shelve is the context manager, so it is properly closed and data is written safely.

The following example shows how can be an object serialization with `shelve`:

```python
import shelve

with shelve.open("students_db") as db:
    db["student:1"] = {"name": "Alice", "age": 21}
    db["student:2"] = {"name": "Bob", "age": 22}
```

Here's an example of deserialization, that is the data loading with `shelve`:

```python
import shelve

with shelve.open("students_db") as db:
    alice = db["student:1"]
    print(alice)
```
