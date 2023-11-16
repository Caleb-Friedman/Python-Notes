Polymorphism is similar to overriding the \_\_init\_\_ method, but you can do it to all methods, not just the constructor

When a method is inherited, it can be rebuilt in a subclass to perform a different task than it was initially designed to do. However, polymorphing the method does not change the method body in the parent class. 

Here is an example of a polymorphed method:
```python
class Animal:
    def speak(self):
        print("Make a sound")

class Cow(Parent):
    def speak(self):
        print("Moo")

animal = Animal()
cow = Cow()

animal.speak()
>>> Make a sound
cow.speak()
>>> Moo
```
> The speak() method was changed in the subclass to print out something different than in the parent class

Even though the methods have the same parameters and the same name, the method is "polymorphed" in the subclass to print out "Moo" rather than "Make a sound." 

No matter how many subclasses there are of a specific parent class, each subclass can polymorph the same parent class method into different things. Take this, for example, where we make two more subclasses of the parent class Animal, each with other speak() forms:
```python
class Animal:
    def speak(self):
        print("Make a sound")

class Cow(Parent):
    def speak(self):
        print("Moo")

class Dog(Parent):
	def speak(self):
		print("Woof")

class Cat(Parent):
	def speak(self):
		print("Meow")
animal = Animal()
cow = Cow()
dog = Dog()
cat = Cat()

animal.speak()
>>> Make a sound
cow.speak()
>>> Moo
dog.speak()
>>> Woof
cat.speak()
>>> Meow
```
However, if a method from a parent class is not overridden in the child class, calling the method on an object of the child class will use the method from the parent class as demonstrated here:
```python
class Animal:
    def speak(self):
        print("Make a sound")

class Cow(Parent):
    def speak(self):
        print("Moo")

class Fox(Parent):
	pass
	
animal = Animal()
cow = Cow()
fox = Fox()

animal.speak()
>>> Make a sound
cow.speak()
>>> Moo
fox.speak()
>>> Make a sound
```