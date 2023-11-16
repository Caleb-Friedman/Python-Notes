Now that we have a firm grasp of the basics of python inheritance and how inheritance works in Object Oriented Programming, we can move on to more advanced topics with Inheritance.
### Overriding
Remember back in the Simple Inheritance notes, we made a new constructor for the Square class. That method actually overrides the Rectangle's constructor in the subclass.

To put it simply, when we have an empty subclass, it inherits the constructor of the parent class like this:
```python
class Rectangle:
	def __init__(self, length, width):
		self.length = length
		self.width = width

class Square(Rectangle):
	pass

sq = Square(5, 5)
```

Now when we made our new constructor in the Square class, it no longer inherits the Rectangle's constructor.
```python
class Rectangle:
	def __init__(self, length, width):
		self.length = length
		self.width = width

class Square(Rectangle):
	def __init__(self, side):
		self.length = side
		self.width = side
	
sq = Square(5, 5)
>>> TypeError: Square.__init__() takes 2 positional arguments but 3 were given
```
> We have successfully overridden the Rectangle's constructor
### The "super" keyword
The super keyword is the way for subclasses to call constructors, of their superclass.

To call a parent class's method, use this syntax instead
	super().methodName()

Lets practice this by calling a parent class's constructor. Here we have a Rectangle parent class and Square subclass. Inside the Square's constructor we call the Rectangle's constructor:
```python
class Rectangle:
	def __init__(self, length, width):
		self.length = length
		self.width = width

class Square(Rectangle):
	def __init__(self, side):
		super().__init__(side, side)
	
sq = Square(5)
print(sq.length)
>>> 5

print(sq.width)
>>> 5
```
> The `super().__init__(side, side)` Is essentially running this line:
> `Rectangle(side, side)` since super() in this context is calling the Rectangle class with the parameters side, side. The `side` parameter is gotten when the Square constructor is called.

Lets run through this process step by step:
1) `sq = Square(5)` --> calls the Square constructor with the parameter side equaling 5
2) `def __init__(self, side)` --> the previous step causes this constructor to run with side = 5
3) `super().__init__(side, side)` --> this calls the Rectangle's constructor with the length parameter equaling side and the width parameter equaling side. Remember, in the first step we assigned side equal to 5
4) `def __init__(self, length, width)` --> the previous step causes the Rectangle constructor to run with the length parameter being 5 and the width parameter being 5
5) `self.length = length` --> assigns the length attribute to the value of the length parameter, which is 5
	`self.width = width` --> assigns the width attribute to the value of the width parameter, which is 5
### Multiple Inheritance
Python allows us to inherit multiple parent classes into a single subclass. This practice however, is very frowned upon within the python community but there is some worth to inheriting multiple classes into one.

For example, we can mix two classes into one class by creating a "mixin class". A mixin class is a fancy name for a class who only inherits from two classes and has no other functionality. It just combines the functionality of two existing classes.

Lets make a mixin class, but first we need to make our parent classes. For this we will just use two barebones classes:
```python
class ParentOne:
	def __init__(self, attributeOne):
		self.attributeOne = attributeOne
		
class ParentTwo:
	def printMessage():
		print("Hello There")
```
> Now we have two parent classes, named "ParentOne" and "ParentTwo". ParentOne has the attribute "attributeOne" and ParentTwo ha s the method printMessage

Now lets make the mixin class:
```python
class MixinClass(ParentOne, ParentTwo):
	pass

myMixin = MixinClass(6)

print(myMixin.attributeOne)
>>> 6
myMixin.printMessage()
>>> Hello There
```
