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

In Python, the module operator for strings (`%`) is an older way to format strings (often called printf-style formatting, from the C programming language). It works by inserting values into placeholders inside a string.

On the left of the `%` there is a string with format specifiers, meanwhile on the right there is a tuple with one, or more elements: position by position, the corresponding format specifier of the string is replaced with the element of the tuple. A format specifier is a substring specifies how the element should be printed to the standard output, or should be represented.

The most common format specifiers are:

- `%s` for the strings (invokes the built-in function `str()` on the element to print). `%10s` means a right align with a minimum of `10` positions, `%-10s` means a left align with a minimum of `10` positions.
- `%r` for the strings also (but it invokes the built-in function `repr()` on the elemenet to represent).
- `%d` for the integers with `10` base (the default base). You can use a padding, for example `%10d`: it means you have `10` positions for the number.
- `%i` for the integers also, with `10` base (the default base); it's an alias for `%d`.
- `%f` for the floating-point numbers. For this format specifier you can set the number of positions for both integer digits and decimal digits: `%6.2f` means you have a width of `6` for the number, but `2` of these positions are for the decimal digits. Both numbers are optional: `%.2f` contraints only the width of the decimal part, `%6f` contraints the width of the entire number.
- `%e` uses the e-notation (or scientific notation) to print a number. Tipically it's used with the floating-point numbers, or with too big, or too short numbers.
- `%x` and `%X` for an hexadecimal number: first prints the letter digits in lowecase, meanwhile second prints the letter digits in uppercase.
- `%o` for an octal number.
- `%%` for the `%` literal in the stirng.

For example:

```python
print("%s is a friend of %s" % ("Alice", "Bob")) # "Alice is a friend of Bob"
```

The first element of the tuple literal, `"Alice"`, take the position of the first `%s` (the first format specifier present in the string). The second element of the tuple literal, `"Bob"`, take the position of the second `%s` (the second format specifier present in the string). If there is an only one format specifier in the string, you can avoid using a tuple and you can specify directly the element:

```python
print("%s is my friend" % "Alice") # "Alice is my friend"
```

There is much more to say on this topic, but please refer to the official Python documentation.

### 09.07. Formatting with `.format()` method

Another way to print to the standard output a formatted string is by using the `.format()` method, directly invoked by the string instance. If you have a variable of the string data type called `aStr`, you can format the string with `aStr.format()`. `aStr` contains zero, one, or more format specifier, in this case represented by the curly brackets: `{}`.

For example:

```python
print("{} is {} years old".format("Alice", 25)) # "Alice is 25 years old"
```

The `.format()` method accepts var args, a variable number of arguments, one for each format specifiers in the `aStr`. If you pass more values as arguments, the exccedeed value are ignored by the `.format()` method. If you pass less values as arguments, you will give an `IndexError`, something similar to this:

```bash
ERROR! IndexError: Replacement index 1 out of range for positional args tuple
```

You can use format specifier into the curly brackets with `.format()`. The most common specifiers are listed here.

- `{}`: apply a default formatting for any data type.
- `{:d}`: apply an integer format, used for integers.
- `{:f}`: apply a floating-point format, used for floating-point numbers.
- `{:.2f}`: apply a floating-point format, with `2` digits for decimal.
- `{:x}`: apply an hexadecimal format with lowercase letters.
- `{:X};: apply an hexadecimal format with uppercase letters.
- `{:o}`: apply an octal format.

With `.format()`, you can use a positional indexing by specifying an inedex into the curly brackets:

```python
print("{2} {0} {1}".format("a", "b", "c")) # "c a b"
```

The position starts from `0` (the first argument of `.format()`) and ends to the length of the arguments list, decremented by `1`. In the previous example, `{2}` refers to the third argument, `"c"`; `{0}` to the first argument, `"a"`; `{1}` to the second argument, `"b"`.

You can use also the named arguments:

```python
print("{name} is {age} years old".format(name = "Alice", age = 30)) # "Alice is 30 years old"
```

There is much more to say on this topic, but please refer to the official Python documentation.

### 09.08. Formatting with `f""` (f-strings)

The best way to format a string in Python3 are the f-strings. An f-string is a string with an `f` as prefix and containing zero, one, or more format specifiers. The main difference with the `.format()` is the way you can bind values, or variables to the format specifiers: in f-strings, you can esily put their identifier into the curly brackets. In this way, you can specify both variable (or value) and format specifiers in the same point (into the curly brackets).

Here's an example:

```python
name = "Bob"
age = 30
print(f"{name} is {age} years old") # "Bob is 30 years old"
```

f-strings can use the following format specifiers:

- `{var}`, where `var` is an identifier of a variable. It's the most common used.
- `{var!r}`: invoke the `__repr__()` method of `var`.
- `{var:d}`: apply an integer format.
- `{var:f}`: apply a floating-point format.
- `{var:x}`: apply an hexadecimal format with lowercase letters.
- `{var:X}`: apply an hexadecimal format with uppercase letters.
- `{var:o}`: apply an octal format.
- `{var:e}`: apply the e-notation (or scientific notation).

You can specify width and alignment. The specifier `{var:>10}` means a right alignment with a maximum of `10` positions. The specifier `{var:<10}` means a left alignment with a maximum of `10` positions. The specifier `{var:^10}` means a center alignment with a miximum of `10` positions. `{var:0>5}` means a maximum of `5` position with a right alignment, but the empty positions are `0`.

The f-strings are like a mini-language you can use directly into the Python programming language. There would be so many things to say, but there isn't enough space (and time) to say them. So let's refer to the official Python documentation, which is certainly exhaustive.
