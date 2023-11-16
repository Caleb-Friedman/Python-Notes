Abstract classes are special classes that **cannot** create objects and can contain abstract methods. These classes must be inherited as they do not have constructors and can contain abstract methods. Abstract methods are methods without a body, the body is given in the subclasses that extend the abstract class.

To create an abstract class, there a few steps you need to follow:
1) Import the ABC class and abstractmethod decorator
2) Inherit the ABC class in the class you want to make abstract

The import line would look like this:
```python
from abc import ABC, abstractmethod
```
> This takes the ABC class and abstractmethod decorator from the abc library and adds it to your code

An example of inheriting the ABC class would look like this:
```python
class myAbstractClass(ABC):
	pass
```

if we try to make an object of an abstract class, it would look like this:
Try running it in your IDE
```python
class myAbstractClass(ABC):
	pass

obj = myAbstractClass()
```
> It worked? You lied to me, I can make objects from abstract classes
> Well, yeah, as long as there are no abstract methods in the class
## Abstract Methods
Inside of abstract classes, you can create abstract methods which are methods without a body. These methods must be created inside the subclasses that extend the abstract class. However, not all methods in abstract classes need to be abstract. Concrete methods like the ones you make in normal classes, can also be inside abstract class. 

The reason to create an abstract method would be to create a framework that includes a method that will change depending on the subclass. A good example of this would be a method to calculate the area of a shape. All shapes have a way of calculating area, but each has a different way of calculating the area.

### The @abstractmethod decorator
To create an abstract method, we have to specify the @abstractmethod decorator above the method. Decorators are a complex topic but essentially, they are things you can add to a method to make them perform slightly differently than usually.

To declare a method with a decorator, add the decorator to the line above the method declaration:
```python
@abstractmethod
def myAbstractMethod():
	pass
```

Abstract methods are methods with no body, the body is implemented in the subclass that inherits the abstract class the method is built in. So the body should only include `pass`.

Now lets put it all together:
```python
from abc import ABC, abstractmethod

class myAbstractClass(ABC):
	@abstractmethod
	def myAbstractMethod(self):
		pass
```

If we try and make an object of the myAbstractClass now, it will give us an error:
```python
object = myAbstractClass()
>>> TypeError: Can't instantiate abstract class myAbstractClass with abstract method myAbstractMethod
```
> So I didn't completely lie to you

## Inheriting Abstract Classes
To completely understand this, make sure you have a firm grasp on the contents of the Simple Inheritance, Advanced Inheritance and Polymorphism note pages. 

Inheriting an abstract class is basically the same as inheriting a regular class like you have done many times. The only difference is that now you have to implement the abstract methods inherited from the parent class. Its very similar to polymorphing methods, instead this time you HAVE to do it.

For an example, lets use shapes. Lets first make the Shape abstract class with two abstract methods, calculateArea() and \_\_init\_\_:
```python
from abc import ABC, abstractmethod

class Shape(ABC):
	@abstractmethod
	def __init__(self):
		pass
	
	@abstractmethod
	def calculateArea(self):
		pass
```
> Dont forget to import abc and inherit ABC in the shape class

Now lets make a Circle class which inherits Shape. We have to build the \_\_init\_\_ and calculateArea methods:
```python
class Circle(Shape):
	#Building the abstract method __init__
	def __init__(self, radius):
		self.radius = radius

	#Building the abstract method calculateArea
	def calculateArea(self):
		print(self.radius * self.radius * 3.14)

circle = Circle(5)
circle.calculateArea()
>>> 78.5
```
> Now we can create objects of the Circle class and call the inherited methods

Just to drive the point home, lets create a Rectangle class which inherits from Shape:
```python
class Rectangle(Shape)
	def __init__(self, length, width):
		self.length = length
		self.width = width
	
	def calculateArea(self):
		print(self.length * self.width)

square = Square(4, 5)
square.calculateArea()
>>> 20
```
## Why Use Abstract Classes?
In the case of making a bunch of classes with a set of common methods and attributes, but you don't want to be able to make an object of the parent class, use an abstract class. Other use cases for abstract classes is to get a higher level of abstraction in your code and hiding important features that could risk security.
