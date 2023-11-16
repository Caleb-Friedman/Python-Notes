Like many other programming languages, python gives functionality to read and manipulate files inside of the operating system's file hierarchy. In this page, we will go over how to open, read and write to text files on the system.

## The `open` Function
The first step in file handling is actually opening the file that we want to use in the program. To do this, python provides us the `open` function. To use it, we write `open()` and inside the parentheses, you specify the path to the file. This could either be the absolute or relative path.

The open function takes in two parameters, the path to the file and the mode to open the file. Here are the possible modes you can open the file in:
- r --> read mode --> reads from the file only
- w --> write mode --> erases the file and allows you to write to the blank fille
- a --> append mode --> allows you to write additional things into an existing file
- rb --> binary read mode --> read mode for images and executables
- wb --> binary write mode --> write mode for images and executables

Whenever you use the `open` function, make sure to assign its output to a variable, so we can use the now opened file.

Using the `open` function:
```python
file = open("C:\path\to\file.txt", 'r')
```
> Opens the file.txt file in read mode and assigns it to the variable `file`

###### DO NOT FORGET: WHENEVER YOU OPEN A FILE, CLOSE IT!!
To close a file, use the `.close()` method on the file object:
```python
file.close() 
```

## Writing to Files
Yeah I know its quite strange to start with writing to files rather than reading them, but if you were to follow along with the code, it is easier this way. 

The first thing you need to do when you want to write to a file is decide whether you want to overwrite the existing text in the file or not. If you do and you want to have a blank file to write to, you open the file in 'write' mode. If you want to keep the existing text in the file, you open the file in 'append' mode.

If you ever open a file that doesnt exist in write mode, the computer will automatically create the file in the specified location. If the absolute path is not given, but rather just the file name, it will create the file in whichever directory the python file is in. 

Opening a file in write mode:
```python
file = open("filename.txt", 'w')
```

Now that we have our file opened, we can use the `.write()` method on the file object to write text to the file like this:
```python
file = open("filename.txt", 'w')

file.write("Writing this to the file")

file.close()
```

Now our program will have no output, but if we look into the text file `filename.txt`, we will see that we have written a line inside of it:
![[file_example.png]]

Just to drive the point home, lets write some more text into our file, but this time lets use the 'append' file mode. One thing to note here is that file.write() does not add a new line after the text:
```python
file = open("filename.txt", 'a')

file.write("Not writing this on a new line")
file.write("\nMust use a newline character")

file.close()
```

Now if we open the file, it will show this:![[Screenshot 2023-10-10 155417.png]]
> As shown with the `\n`, .write() does acknowledge escape characters.
 
> Since we opened the file in 'append' mode, the "Writing this to a file" is still there

## Reading Files
Cool, we can write to files, but what if we wanted to use something written to a file in our program? Well, for that we can read from files by opening the files in 'read' mode. If the file is a text file or other file types that contain strings, we can open it in 'r' mode, but for images and file types that contain machine code, we open the file in 'rb' mode.

Lets open the `filename.txt` file we used earlier in read mode:
```python
file = open("filename.txt", 'r')
```

If we want to read from a file, we have a few methods to do that:
- .read() --> returns the entire file as a string
- .readline() --> returns the next line of the file as a string
- .readlines() --> returns a list of strings, where each string is a single line of the file

For this example, we will be using the .readline() method, as the .readlines() will not work for larger files and .read is mostly for binary files:
```python
file = open("filename.txt", 'r')

print(file.readline())
>>> Writing this to the fileNot writing this on a new line

file.close()
```

If we have a lot of lines in our files, it is good practice to use a for loop to loop through the lines of the files. When you loop through a file object, the iterator will be set equal to each line. So on the first loop, the iterator will be set to the first line of the file, the second loop its the second line and so on.

Using a for loop to print the contents of a file:
```python
file = open("filename.txt", 'r')

for line in file:
	print(line)

file.close()

>>> Writing this to the fileNot writing this on a new line
>>> Must use a newline character
```
> In this case, `line` is the iterator

## The `with` Keyword
I'm sure I was not the only one who was extremely confused when the professor started talking about the `with` keyword automatically calling some functions. After he started talking about those I basically zoned out, so let me explain the `with` statement in more simple terms.

When using the `with` statement to open files, the file will automatically close when the `with` block ends, removing the need to always put in the file.close() line. To use the `with` statement, the syntax is slightly different than opening the file usually.

The new syntax is like this:
```python
with open("filename.txt", 'r') as file:
	pass
```
> All the code using the file should be indented inside the `with` block

Lets use the `with` statement to print out the lines of a file using a for loop:
```python
with open("filename.txt", 'r') as file:
	for line in file:
		print(line)

>>> Writing this to the fileNot writing this on a new line
>>> Must use a newline character
```

Now that we got understand `with` in a simple way, lets try and dissect the `with` statement's functionality in a more complicated way. Remember how there are some python functions which are special? The functions that always start and end with double underscores like \_\_init\_\_ and \_\_str\_\_? If not, refer to the **Using Built-in Classes and Functions note page**.

Some objects have the methods \_\_enter\_\_ and \_\_exit\_\_, which are special methods for the `with` statement. The file object has these methods, and inside of the file class's \_\_exit\_\_, it closes the file which is why we don't need to manually close the file with `file.close()`.

If we create a collection-type object and give it \_\_enter\_\_ and \_\_exit\_\_ methods, we can create those objects using a `with` statement. To explain this, lets create a class using the `list` built-in class:
```python
class ExampleClass(list):
	pass
```

Now lets give it the \_\_enter\_\_ and \_\_exit\_\_ methods:
```python
class ExampleClass(list):
	def __enter__(self):
		print("Executing the enter function")
		return self

	def __exit__(self, type, value, tb):
		print("Executing the exit function")
```
> Why do we have to return self? What are the parameters `type`, `value` and `tb`? 
> Dont worry, we will cover these soon.

Lets create an ExampleClass object using a `with` statement:
```python
with ExampleClass() as EC:
	EC.append(1)
	EC.append(2)
	EC.append(3)
	print(EC)

>>> Executing the enter function
>>> [1, 2, 3]
>>> Executing the exit function
```

So now that we see how the \_\_enter\_\_ and \_\_exit\_\_ function are run when calling a `with` statement, now we can talk about the special syntax for the aforementioned functions. 

So for the \_\_enter\_\_ function, we have to return self or else the `with` statement will not assign the object created as the type, and instead it will be NoneType. Yeah, but in simple terms? Essentially, in the above example, EC will not be an object of ExampleClass. Lets show that:
```python
class ExampleClass(list):
	def __enter__(self):
		print("Executing the enter function")
		#No return self here

	def __exit__(self, type, value, tb):
		print("Executing the exit function")
		
with ExampleClass() as EC:
	print(type(EC)) #Checking if EC is an ExampleClass type
	EC.append(1)
	EC.append(2)
	EC.append(3)
	print(EC)

>>> Executing the enter function
>>> <class 'NoneType'>
>>> Executing the exit function
>>> AttributeError: 'NoneType' object has no attribute 'append'
```
> As you can see, EC is not an ExampleClass, rather it is a NoneType object instead.

The \_\_exit\_\_ function takes in four parameters: self and three others. The three other parameters are for if an exception is thrown in the `with` block. The "type" parameter specifies the type of exception, the "value" specifies what triggered the exception and "tb" or "traceback" specifies where the traceback object is. If there is no exception in the `with` block, all of these parameters are assigned None.

To show this, lets print out the parameters in the \_\_exit\_\_ block:
```python
class ExampleClass(list):
	def __enter__(self):
		print("Executing the enter function")
		#No return self here

	def __exit__(self, type, value, tb):
		print("Executing the exit function")
		print(type)
		print(value)
		print(tb)
		
with ExampleClass() as EC:
	EC.append(1)
	EC.append(2)
	EC.append(3)
	print(EC)

>>> Executing the enter function
>>> Executing the exit function
>>> <class 'AttributeError'>
>>> 'NoneType' object has no attribute 'append'
>>> <traceback object at 0x000002B103350240>
```
> Will you ever use these? Probably not, but the parameters do exist

