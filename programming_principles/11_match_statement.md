# 11. `match` statement

The `match` statement is a multiple selection statement, very similar to the `switch` statement proposed by many others programming languages (like C, C++, Java and PHP).

The `match` statement has the following syntaxt:

```python
match expression:
    case value1:
        statement1
        statement2
        ...
        statementN
    case value2:
        statement1
        statement2
        ...
        statementN
    ...
    case valueN:
        statement1
        statement2
        ...
        statementN
```

After the `match` keyword, there is an expression. This expression can be evaluated as an integer, a boolean, or a string. Inside the `match` block there are many `case` caluses: each clause specify, after the `case ` keyword, the value matching `expression`. Inside each `case` block there are one, or more statements. Python interpreter first evaluates `expression`; second, it compares the result of `expression` with each value present after each `case` keyword: it executes the statement inside the `case` where is specified a value matching the `expression`.

```python
a = 10
match a + 10:
    case 10:
        print("expression is 10")
    case 20:
        print("expression is 20")
    case 30:
        print("expression is 30")
```

The previous snippet of code causes the following output: `"expression is 30"`. If you need to execute one, or more actions in case of no matching, you can use the underscore character (`_`), that means the relative `case` clause is the default clause:

```python
a = 10
b = 50 + a
match b:
    case 10:
        print("expression is 10")
    case 20:
        print("expression is 20")
    case 30:
        print("expression is 30")
    case _:
        print("b is ", b)
```

The previous code produces the string `"b is 60"` as output, because the value `60` (`50 + a`) doesn't match any value of the `case` clauses.

`match` statement allows you to combine a value thanks to the pipe operatore (`|`):

```python
day = 4
match day:
  case 1 | 2 | 3 | 4 | 5:
    print("Today is a weekday")
  case 6 | 7:
    print("Happy weekend!")
```

In the previous code, if the value of `day` is `1`, `2`, `3`, `4`, or `5` (first `case` clause), the output of the program is `"Today is a weekday"`; if the value is `6`, or `7`, the output is `"Happy weekend!"`.
