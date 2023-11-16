Python allows us to define a class that has all the attributes and methods from another class. This creates a Parent - Child hierarchy, and accordingly the class being inherited is called the parent class, and the class inheriting is called the child class. 

To demonstrate this, lets make a class called Rectangle with two attributes, one for the length and width and a method to print its area:
```python
class Rectangle:
	def __init__(self, length, width):
		self.length = length
		self.width = width
	
	def printArea(self):
		print(f"{self.length * self.width}")

rect = Rectangle(4, 10)

rect.printArea()
```

Now lets say we wanted to make a subclass of the rectangle which would be the class Square. To do this, define the class Square, and after the class name, add parentheses and inside of the parentheses, add the class you want to inherit:
```python
class Square(Rectangle):
	pass
```
> There is currently nothing in the class, so we just put pass

Now we can create objects of the square class:
```python
sq = Square(5, 5)

sq.printArea()
>>> 25
```

### Making Subclass Constructors
Now, you may see that we still need to add two parameters when creating a square. Since we inherited the Rectangle constructor, and that constructor has two parameters, we still need two. Inside the Square class we can make its own constructor to override the inherited constructor:
```python
class Square(Rectangle):
	def __init__(self, side):
		self.length = side
		self.width = side

sq = Square(5)

sq.printArea()
>>> 25
```

### New Subclass Methods
You can also add its own methods to the square class. These methods will NOT appear in the Rectangle superclass. You make these methods like how you would make any other method, just put it in the subclass:
```python
class Square(Rectangle):
	def __init__(self, side):
		self.length = side
		self.width = side
	
	def printPerimeter():
		print(self.length * 4)

sq = Square(5)

sq.printArea()
>>> 25

sq.printPerimeter()
>>> 20
```
> The square class has the new constructor, the printPerimeter() method and still has the printArea() method that the Rectangle superclass has

### New Subclass Attributes
Subclasses can also contain its own attributes that the superclass does not. For example, we can add an integer *totalAngleDegrees* in the Square class. If we try to call this attribute on a Rectangle object, it will result in an error:
```python
class Square(Rectangle):
	def __init__(self, side):
		self.length = side
		self.width = side
		self.totalAngleDegrees = 360
			
	def printPerimeter():
		print(self.length * 4)

sq = Square(5)
rect = Rectangle(4, 5)

print(sq.totalAngleDegrees)
>>> 360

print(rect.totalAngleDegrees)
>>> AttributeError: 'Rectangle' object has no attribute 'totalAngleDegrees'
```