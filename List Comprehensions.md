The easiest way to explain list comprehensions is that they are one-liner for loops that create a list. Perhaps you have a list of strings and you want to turn them into integers, sure you can do that with a normal for loop like this:
```python
strings = ["1", "23", "456", "7890"]
integers = []
for i in strings:
	num = int(i)
	integers.add(num)
```

On the surface, there is nothing wrong with this code, it is clean and fairly readable for other python programmers. Yet why write 5 lines of code when you can do this in two lines of code using a comprehension?
```python
strings = ["1", "23", "456", "7890"]
integers = [int(i) for i in strings]
print(integers)
>>> [1, 23, 456, 7890]
```

List comprehensions have this syntax:
`<list_name> = [<expression> for <variable> in <iterable>]`
In the case above lets match the code to the syntax:
- \<list_name\> --> *integers*
- \<expression\> --> *int(i)*
- \<variable\> --> *i*
- \<iterable\> --> *strings*

List comprehensions are basically mini for loops used to create lists. They can also filter things that are added to the list by added an if statement to the end of the comprehension with this syntax:
`<list_name> = [<expression> for <variable> in <iterable> if <expression>]`

Lets say we had the same list of strings from before, but now we want our new list to only contain the integers that are even, we could make a list comprehension like this:
```python
strings = ["1", "23", "456", "7890"]
integers = [int(i) for i in strings if int(i) % 2 == 0]
print(integers)
>>> [456, 7890]
```

Once again lets match the code to the syntax:
- \<list_name\> --> *integers*
- \<expression\> --> *int(i)*
- \<variable\> --> *i*
- \<iterable\> --> *strings*
- \<expression\> --> *int(i) % 2 == 0*

List comprehensions can be extremely complicated to try and decipher, and if you dont feel comfortable using list comprehensions right now, dont worry, you can always just make them as for loops.

