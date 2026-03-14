# 07. Strings

### 09.01. Overview

A string is a collection of ordered characters. A character is a symbol uniquely identified by a code, which depends on the character set used by the language, or the system. Python uses Unicode as character set, it means Python can represent more than 1 milion of characters of all types, languages and cultures.

The Unicode standard proposes three main encodings:

- UTF-8 (uniform Trasformation Format - 8 bit): it can represents more than 250 of characters, it is backwards compatible to the ASCII (American Standard Code for Information Interchange) of 7 and 8 bit (EASCII, Extended ASCII).
- UTF-16 (uniform Trasformation Format - 16 bit): it can represents more than 65k of characters.
- UTF-32 (uniform Trasformation Format - 32 bit): it can represents more than 1 milion of characters.

In Python any strings is enclosed by the double, or single quotes:

```python
"This is a string literal"
'Also this is a string literal'
```

You can use the `print()` built-in function to print a string to the standard output:

```python
a = "Hello, World!\n"
print(a) # "Hello, World!"
```

A string enclosed by the double quotes can contain single quotes, meanwhile a string enclosed by the single quotes can contain double quotes:

```python
"This is 'a string' enclosed by the double quotes"
'This is "a string" enclosed by the single quotes'
```

You can specify a multiline string in the following way:

```python
a = """This
is a multiple
line string"""
print(a)
```

For the multiline strings, you can use both triple single quotes (`'''`) and triple double quotes (`"""`).

The `len()` function returns the length of string, which is the number of characters of the string:

```python
str = "Hello"
print(len(str)) # 5
```

### 09.02. Slicing

You can use the range operator to obtain a substring from the original string:

```python
a = "Hello"
print(a[2:4]) # ll
```

The rules are always the same for the range operator `[n:m]`: both `n` and `m` are optional. If `n` is not present, the default is `0`. If `m` is present, the default is the length of the string.

```python
a = "Hello"
print(a[2:4]) # ll
print(a[:4]) # Hell
print(a[2:]) # llo
```

You can create a copy of the original string by using the range operator with colon only (`:`):

```python
a = "Hello"
b = a[:]
print(b) # Hello
```

You can also use the negative indexes:

```python
a = "Hello"
print(a[-3:-1]) # ll
```

### 09.03. Escape Characters

To insert characters that are illegal in a string, use an escape character. An escape character is a backslash `\` followed by the character you want to insert. An example of an illegal character is a double quote inside a string that is surrounded by double quotes:

```python
"This is an " illegal string" # ERROR!
```

You must use an escape character:

```python
"This is an \" illegal string"
```

Some of the most commons escape characters are the following:

- `\n`: new line.
- `\r`: carrige return.
- `\a`: alert, or "beep".
- `\t`: horizontal tab.
- `\v`: vertical tab.
- `\\`: backslash.
- `\"` double quote.
- `\'`: single quote.
- `\b`: backspace.

Python allows you to specify a Unicode character with three octal digits, or two hexadecimal digits:

- `\ooo`: where `ooo` are the three octal digits. This value starts from `000` to `777`.
- `\xhh`: where `hh` are the two hexadecimal digits. This value starts from `00` to `FF` (or `ff`).

### 09.04. Concatenation

You can use the concatenation operator (`+`) to concatenate two, or more strings:

```python
a = "Hello"
b = "World"
print(a + " " + b + "!") # Hello, World!
```

In Python, in function of the context where the `+` operator is used, it operates in a different way:

- If two operands are numbers (integer, or floating-point), `+` is the sum operator.
- If two operands are strings, `+` is the concatenation operator.

```python
print(10 + 5) # 15
print("Hello, " + "World!") # Hello, World!
```

### 09.05. Methods

Disclaimer: all the following methods don't modify the original string, but they create a copy of original string and operate on it, so they return a new string (the original string is unchanged). In Python, strings are immutable.

`upper()` returns the same string, but in uppercase:

```python
a = "Hello"
print(a.upper()) # HELLO
```

`lower()` returns the same string, but in lowercase:

```python
a = "HELLO"
print(a.lower()) # hello
```

`strip()` returns the same string, but whitout any spaces at the begin, or end:

```python
a = "   Hello!   "
print(a.strip()) # returns "Hello!"
```

`capitalize()` converts the first charatcter in uppercase:

```python
a = "hello"
print(a.capitalize()) # Hello
```

`count()` accepts a string, or a character and returns the number of occurences of the string, or character:

```python
str = "The apple is on the pineapple"
print(str.count("apple")) # 2
```

`endswith()` returns `True` if the string ends with the specified value:

```python
a = "Hello"
print(a.endswith("llo")) # True
print(a.endswith("lli")) # False
```

`startswith()` returns `True` if the string starts with the specified value:

```python
a = "Hello"
print(a.startswith("Hi")) # False
print(a.startswith("He")) # True
```

`find()` sarches the string for a specified value and returns the position of where it was found (the position is an index, an integer value). If the specified value is not present, it returns the value `-1`.

```python
a = "Hello"
print(a.find("llo")) # 2
print(a.find("ll0")) # -1
```

`isalnum()` returns `True` if all characters in the string are alphanumeric:

```python
a = "Hell0123"
print(a.isalnum()) # True
```

`isalpha()` returns `True` if all characters in the string are in the alphabet:

```python
a = "Hello"
print(a.isalpha()) # True
```

`isascii()` returns `True` if all characters in the string are ascii characters:

```python
a = "aeiou"
print(a.isascii()) # True
b = "⑳⑳⑳"
print(b.isascii()) # False
```

`isdecimal()` returns `True` if all characters in the string are decimals:

```python
a = "123"
print(a.isdigit()) # True
b = "FFF"
print(b.isdigit()) # False
```

`isdigit()` returns `True` if all characters in the string are digits:

```python
a = "123"
print(a.isdigit()) # True
```

`isidentifier()` returns `True` if the string is an identifier:

```python
a = "aNum"
print(a.isidentifier()) # True
```

`islower()` returns `True` if all characters in the string are lowercase:

```python
a = "hello"
print(a.islower()) # True
```

`isupper()` returns `True` if all characters in the string are uppercase:

```python
a = "HELLO"
print(a.isupper()) # True
```

`replace()` returns a string where a specified value is replaced with a specified value:

```python
str = "I love pizza"
print(str.replace("pizza", "pasta")) # I love pasta
```

`rfind()` searches the string for a specified value and returns the last position of where it was found, otherwise it returns `-1`:

```python
str = "Pizza Pizza Pizza"
print(str.rfind("Pizza")) # 12
```

`rstrip()` returns a right trim version of the string:

```python
str = "   Hello   "
print(str.rstrip()) # "   Hello"
```

`split()` splits the string at the specified separator, and returns a list:

```python
fruits = "apple,orange,cherry,kiwi"
print(fruits.split(",")) # [ 'apple', 'orange', 'cherry', 'kiwi' ]
```

`zfill()` fills the string with a specified number of `0` values at the beginning:

```python
str = "50"
print(str.zfill(10)) # 0000000050
```

### 09.06. Formatting with `%` operator
<!-- to do -->

### 09.07. Formatting with `.format()` method
<!-- to do -->

### 09.08. Formatting with `f""` (f-strings)
<!-- to do -->
