Whenever something goes wrong in a python program, an error is raised. Errors can be raised for a multitude of reasons, such as dividing by zero, indexing a string or list beyond the end of it, and mistyping variable names. Errors can be very useful for debugging code, so sometimes it is useful to raise your own errors, or catch raised errors to run other code.

## Raising Exceptions
For debugging purposes, or to run except blocks, a programmer can raise their own errors using the `raise` keyword. Raising errors arent the most useful thing to do, but they do have its uses.

To raise an error, follow these steps:
- Write `raise`
- Specify the type of exception (or just write `Exception`)
- Add parentheses
- Inside the parentheses, add a string of text to print out when the error is raised

An example of raising an error:
```python 
raise Exception("This is an exception")
>>> Traceback (most recent call last):
>>> File "<string>", line 1, in <module>
>>> Exception: This is an exception
```

## Try - Catch Blocks
Sometimes when an exception is thrown, we don't want to end the program. For example, if we take integer input from the user, and the user accidentally gives us a letter, we don't want an exception thrown and ending the program. For cases like this, we use a Try - Except statement.

Try - Except works by first running the code in the body of the try. If an error is thrown in the try, the except block runs instead of cutting the program. 

To make a Try - Except statement, follow these steps:
- Write `try`
- Add a colon
- Write the code you want inside the try block indented once
- Unindent and write `except`
- Add a colon
- Write the code you want inside the except block indented once

Here is an example of a Try - Except statement:
```python
try:
	raise Exception("This is an exception")
except:
	print("Caught the bastard")
>>> Caught the bastard
```

You can also specify the type of exception you want to catch, in case you want to differentiate and catch only a certain error. To specify the type of error, just write the name of the error after the `except` statement:
```python
try:
	x = 100 / 0
except TypeError:
	print("Caught a TypeError")
>>> Traceback (most recent call last):
>>>  File "<string>", line 2, in <module>
>>> ZeroDivisionError: division by zero
```
> Since the try block throws a ZeroDivisionError and not a TypeError, the except block doesn't run

You can write multiple except statements for different error types:
```python
try:
	x = 100 / 0
except TypeError:
	print("Caught a TypeError")
except ZeroDivisionError:
	print("Caught a ZeroDivisionError")
>>> Caught a ZeroDivisionError
```

### The Else Block
Similar to how an else block in a if - else statement runs when the if doesn't run, an else block after a Try - Except runs if the except doesnt run. This is useful for continuing code after a successful try, but only if the code shouldn't be run after an unsuccessful try. 

Here is an example of using an else block after a Try - Except:
```python
try:
	x = 100 / 10
except:
	print("Caught the bastard")
else:
	print("No bastard to be caught")
>>> No bastard to be caught
```
### The Finally Block
We can use the finally block if you want some code to run regardless of an error in the try block. Whether the except block runs or not, the finally will always run.

To add a finally block to the code, find where the body of the except block ends, write finally, and add curly braces. Anything inside those curly braces will run regardless of whether the except statement runs.

Here is an example of a finally running when an except block *IS NOT* run:
```python
try: 
	x = 100 / 10
except:
	print("Caught the bastard")
finally:
	print("Was the bastard caught?")
>>> Was the bastard caught?
```

Here is an example of a finally running when an except block *IS* run:
```python
try: 
	x = 100 / 0
except:
	print("Caught the bastard")
finally:
	print("Was the bastard caught?")
>>> Caught the bastard
>>> Was the bastard caught?
```

You can combine these blocks in many different ways, here is a list of all the usable combinations:
- Try - Except
- Try - Finally
- Try - Except - Else
- Try - Except - Finally
- Try - Except - Else - Finally

Some combinations are not allowed:
- Try - Else
- Try - Else - Finally
> Essentially, the else block requires an except