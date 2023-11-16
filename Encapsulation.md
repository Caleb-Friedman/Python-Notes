In programming, it is quite often that you will hand over your code to someone else, and they will try to debug and fix your code. When this happens, this could lead to some problems when they change class attributes. For example, say you have a class variable called *num* and you dont want this variable to be changed. There is nothing stopping another person from creating an object of the class and changing the value that *num* is set to:
```python
class MyClass:
	num = 15

obj = MyClass()
obj.num = "asuguih"

print(obj.num)
>>> asuguih
```

To stop this, we can use Encapsulation to protect our variables from reckless changes. Encapsulation entails two methods that we should use when accessing and assigning attributes: **Getters & Setters**.

A getter method is quite simple, all it does is return the variable specified:
```python
class MyClass:
	num = 15
	 
	# Getter method for the attribute *num*
	def get_num(self):
		return self.num

obj = MyClass()

print(obj.get_num())
>>> 15
```

A setter method does exactly what you think it will do, it takes in an argument, and assigns an attribute to the argument:
```python
class MyClass:
	num = 15
	
	# Getter method for the attribute *num*
	def get_num(self):
		return self.num
	
	# Setter method for the attribute *num*
	def set_num(self, num):
		self.num = num

obj = MyClass()

obj.set_num(30)

print(obj.get_num())
>>> 30
```

But do these actually stop people from changing the variable manually like was shown in the first example? Sadly not. Some of you may think, "is there a way we can set variables to private?", the answer is no. Sometimes, two underscores before a variable name works, but in Thonny, the IDE we learned last semester, that is not the case:
```python
class MyClass:
	__num = 15
	
	# Getter method for the attribute *num*
	def get_num(self):
		return self.__num
	
	# Setter method for the attribute *num*
	def set_num(self, num):
		self.__num = num

obj = MyClass()

obj.__num = 45

print(obj.__num)
>>> 45
```

To combat this, python has created a convention that all variables which start with one underscore should be treated as private. This is not enforced by the interpreter though.
