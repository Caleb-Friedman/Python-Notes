All of the exceptions that we have handled in the Error Handling section of the notes are exceptions inherited from the Exception class. However, not all exceptions are like this, some inherit directly from the BaseException class instead. All exceptions inherit from the BaseException class, either directly or through the Exception class which itself inherits from the BaseException class.![[Exception_Heirarchy_Diagram.png]]

## Special Exceptions
The special exceptions here are defined as exceptions that directly inherit the BaseException class rather than inheriting the Exception class. We will go over two of these special exceptions, the SystemExit and the KeyboardInterrupt exceptions.
### SysExit Exception
This is the exception that is thrown whenever a sys.exit() function is called within the program. Generally, this function just stops running the program, but we can catch it if we want to do some cleanup before the program ends. However, since we cant use the `finally` to clean up the code due to the nature of this exception, we usually don't try to catch it.
### KeyboardInterrupt Exception
This exception is quite common when using python as a command-line scripting language. Whenever the user enters Control + C while running a python script on the command-line, a KeyboardInterrupt Exception is raised.

## User-Defined Exceptions
If none of the other types of exceptions fit the circumstance in which you want to raise them, you can create your own types of exceptions. These exceptions, often called custom exceptions are exceptions you define and can raise using the `raise` keyword. If you need a refresher on `raise`, there is a section about it in the Error Handling notes.

To create your own exception, you first need to create a class named whatever you want the exception to be named. After that, you need to inherit the `Exception` class like this:
```python
class YourException(Exception):
	pass
```

After that, you don't really need to add anything else to the class unless you want a constructor that does something other than print out a line of text, so in this case, we can just put `pass` for the class body.

Now that we have our own Exception class, we can raise an exception of that type with the `raise` keyword like this:
```python
raise YourException("Raising my own Exception")
>>> Traceback (most recent call last):
>>>  File "<string>", line 4, in <module>
>>> YourException: Raising my own Exception
```

### Custom Constructors
Lets say you want to do more than just print out a line of text when your custom exception is raised. To do this, we need to polymorph the Exception class's \_\_init\_\_ method. 

For an example lets make an error that is thrown whenever a given number is odd. When the error is raised, we want it to say "The given number, {the name of the number}, cannot be odd". 

First, we need to make the custom error's class:
```python
class CantBeOdd(Exception):
	pass
```

Next, we can polymorph the inherited \_\_init\_\_ function. We need to take in the number that was odd, so we add `num` as an extra parameter in the constructor:
```python
def __init__(self, num):
	pass
```

Inside of our polymorphed \_\_init\_\_ method, we can use the super keyword to call the constructor of the Exception class with the string we want to print:
```python
def __init__(self, num):
	super().__init__(f"The number given, {num}, cannot be odd")
```

Now whenever we raise our new error, we have to pass in the number and it will print our custom message:
```python
x = 11
if x % 2 == 1:
	raise CantBeOdd(x)
else: 
	print(f"The number, {x} is even")
>>> Traceback (most recent call last):
>>>  File "<string>", line 7, in <module>
>>> CantBeOdd: The number given, 11 cannot be odd
```

### User Defined Exception Attributes
If you ever wanted to store a piece of data into an attribute of an exception class, you will be delighted to hear that you can. Generally, you need to catch these exceptions that you raise if you want to make use of these attributes. If you dont catch the error, the program will just end before you are able to use these attributes.

Lets add an attribute to the CantBeOdd exception class which stores the `num` parameter. You can do this just like how you create attributes in regular class's constructors:
```python
class CantBeOdd(Exception):
	def __init__(self, num):
		super().__init__(f"The given number, {num} cannot be odd")
		self.storedNum = num
```
> If you need a refresher on class attributes, check the Classes notes page

Before try to raise and catch this error, we need to add something to our try - except statement. If we just wanted to catch the CantBeOdd error, you would think we can do it like this:
```python
try:
	#Code here
except CantBeOdd:
	#More code here
```
If we do it like this, we are not able to access the attributes stored inside the CantBeOdd class object, since we dont create the object. To create the object, we need to add an `as <name>` statement seceding the exception type in the `except` line like this:
```python
try:
	#Code here
except CantBeOdd as e:
	#More code here
```
> Generally, programmers name their exception class objects `e`

Now lets catch this exception and make use of the storedNum attribute:
```python
x = 11

try:
	if x % 2 == 1:
		raise CantBeOdd(x)
	else: 
		print(f"The number, {x} is even")
except CantBeOdd as e:
	print(f"The stored number is: {e.storedNum}")
>>> The stored number is 11
```

