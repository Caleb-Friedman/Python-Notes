Since Python is an Object-Oriented Programming language, it can support classes and objects. Much we have done so far has been through classes, even if you didn't know. For example, Scanner, Random, and String are all Python classes from which we have created objects. 

## Object Oriented Programming
In programming, an object is a collection of variables, called attributes, and functions, called methods. The attributes are the characteristics of the object, and the methods are the actions the object could perform. 

We often use classes to represent real-world items like phones, animals, books, etc. A typical example would be a car object. A car has attributes like its color, model, manufacturer, the year it was built, and actions such as driving, braking, and honking.

Classes create a blueprint for objects: they define the particular attributes each class object will have. Whenever you create an object of a class, the code will specify the attributes in that instance of an object.

An instance is essentially one object of a class. If you have two objects of a car class, you have two car instances. Each instance can have different attributes assigned to them. For example, if the car class has a string attribute called color, one instance can have the color attribute equal to "blue" while another has the attribute equal to "white".

## Creating a Class
Creating a class is as simple as writing *class* and then the name you want to assign the class. If we wanted to make an empty class, we have to use the keyword *pass*. An example of creating a class is shown here:
```python
class MyClass:
	pass
```
> Just like loops, conditionals and functions, you indent when inside of a class

To create an object of a class, follow these steps:
- Name the object like you are naming a variable
- Equal sign
- Specify the class name again
- Add a pair of parentheses

Here, we make two objects of the *MyClass* class:
```python
object_1 = MyClass()
object_2 = MyClass()
```
> This code must not be inside of the class

The above code combined would look like this:
```python
class MyClass:
	pass

object_1 = MyClass()
object_2 = MyClass()
```

### Class Attributes
Now we can start adding things to our class, lets start with a variable. Inside of the class we can declare variables which we will later be able to reference using objects of the class. These variables that are created inside of classes have a special name: **Attributes** For example, here is a class with a variable called *num*:
```python
class MyClass:
	num = 12
```

Now if we want to access this variable, we have to create an object of the class, and call it using the following steps:
- Specify the class name
- Period
- Specify the attribute name

Here is an example of calling the *num* attribute from the class *MyClass*:
```python
class MyClass:
	num = 12

object_1 = MyClass()

print(object_1.num)
>>> 12
```
> In this document, >>> is used to show output

Classes can have multiple attributes, and the attributes can be changed with operators like we did last year. If you change an attribute of one class object, it **WILL NOT** change the attribute for the other class objects. For example:
```python
class MyClass:
	num = 12
	string = "Amnesiac"

object_1 = MyClass()
object_2 = MyClass()

object_1.num = 34;

print(object_1.num)
print(object_2.num)
>>> 34
>>> 12
```

### Class Methods
Now that we have gotten the hang of creating class variables, lets create some class functions. Functions that belong to objects also have a special name: **Methods**. 

If you need some help remembering all the intricacies of python functions, w3schools has a quick refresher of everything function-related we learned in COP 2512: [Function Review](https://www.w3schools.com/python/python_functions.asp) 

Calling a class method is quite similar to calling a function, however, you have to use the dot syntax that was mentioned earlier in the [[#Class Attributes]] section. Follow these steps to call a class method:
- Create an object of the class
- Specify the name of the object
- Period
- Specify the name of the method
- Open Parentheses
- Specify the arguments (if needed)
- Close Parentheses
- Colon

Lets add a method to our *MyClass* class:
```python 
class MyClass:
	num = 12
	string = "Amnesiac"
	
	def myMethod(self):
		print("Hello World")
	
obj = MyClass()

obj.myMethod()

>>> Hello World
```

### The "self" Parameter
As you may have noticed in the code above, we have a parameter in the method *myMethod*. You may have also noticed that the method call does not provide an argument for the parameter. This is because the "self" a reference to the instance of the class that called the method. It is used when referencing variables that belongs to the class, similar to the "this" keyword in Java.

Here is an example of using the "self" parameter:
```python
class MyClass:
	num = 12
	string = "Amnesiac"
	
	def myMethod(self):
		print(f"Hello {self.string}")
	
obj = MyClass()

obj.myMethod()

>>> Hello Amnesiac
```

### Class Constructors
A class constructor is a special method in classes that is exclusively called when an object of the class is created. Whenever you instantiate a class object, you call the constructor. By default, all classes start with an empty constructor to create objects of that class. This empty constructor is not specifically in the code but is used whenever you create an object of a class with no specified constructor. Constructors have no return statement, but can take in parameters.

Specified constructors can take in parameters and assign attributes values. To create a specified constructor, follow these steps:
- Write def
- Write \_\_init\_\_
- Add parentheses
	- Inside the parentheses, specify the parameters including [[#The "self" Parameter]]
- After the parentheses, colon.

Yes, all constructors must be named \_\_init\_\_, this is because this is one of the [[#Special Python Methods]]. All of these special methods do something that normal methods dont and have the \_\_ syntax. 

Here is an example of creating a python constructor:
```python
class MyClass:
	num = 0
	
	def __init__(self):
		self.num = 10
	
obj = MyClass()

print(obj.num)
>>> 10
```

It is good practice to instead of creating an attribute outside the constructor and assigning it in a constructor, you just create the variable inside the constructor like this:
```python
class MyClass:
	def __init__(self):
		self.num = 10
	
obj = MyClass()

print(obj.num)
>>> 10
```

The most common use of constructors is assigning values to attributes when a class is created. Lets say we have a *Person* class that needs a first and last name, inside the constructor we can take in parameters for the first and last names and assign them to attributes. 
```python
class Person:
	def __init__(self, first, last):
		self.first = first
		self.last = last

person_1 = Person("Jace", "Beleren")
person_2 = Person("Liliana", "Vess")

print(person_1.first)
print(person_2.last)
>>> Jace
>>> Vess
```

### Special Python Methods
Python has some special methods that can be added to you classes. These special methods a special syntax, they all have two underscores before and after the method name, for example: \_\_init\_\_  and \_\_str\_\_. 

### The \_\_str\_\_ Method
Before I start explaining what is this method's special function, lets try to print an object of a class:
```python
class MyClass:
	pass
	
obj = MyClass()
print(obj)
>>> __main__.MyClass object at 0x00000263A420BA00>
```
> What is that?
> That is a memory address

I assume when you want to print out an object of a class, you dont want a memory address to be printed. In that case, we can use the 
\_\_str\_\_ method to specify what we want printed. The method is declared with "self" as the only parameter, and it returns what you want to print when an object of the class is printed.

Here is an example of creating and using the \_\_str\_\_ method:
```python
class MyClass:
	def __str__(self):
		return f"Printing"
	
obj = MyClass()

print(obj)
>>> Printing
```

