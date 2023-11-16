## Getters and Setters
In many programming languages, we are told to never access class attributes by calling the attribute, instead, we make getter and setter methods to return and update the attribute. One of these languages is Java, but in Python, we dont need these methods to keep in convention.

Code with getter and setter methods would look like this:
```python
class MyClass:
	def __init__(self, attribute): # Constructor
		self.attribute = attribute

	def get_attribute(self): # Getter
		return attribute

	def set_attribute(self, value): # Setter
		self.attribute = value

obj = MyClass(12)
print(obj.get_attribute())
>>> 12
obj.set_attribute(34)
print(obj.get_attribute())
>>> 34
```
> We will refer to this as the "Method Syntax"

Instead of the above, the correct Python convention would not be using getter and setter methods and instead just accessing the attribute:
```python
obj = MyClass(12)
print(obj.attribute)
>>> 12
obj.attribute = 34
print(obj.attribute)
>>> 34
```
> We will refer to this as the "Simpler Syntax"

In languages where it is convention to make all attribute private, we need this to create a public interface for the attributes we want to be used outside of the class. Put simply, you cannot access attributes directly, and instead must access them though methods.

Since python has no real `private` access modifier, we dont need to follow this convention that is quite common in other languages. 

## The `property` Function
There is no easy way to explain the `property` function, so you may need to read this section a few times over for it to really click. Essentially, the property keyword takes semi-private (_ before method name) getter and setter methods for an attribute and uses those methods when updating and returning the attribute while using the Simpler Syntax.

The way to make the `property` keyword work is by following these steps:
- Declare the class and create the constructor
- Declare the attribute in the constructor as semi-private
- Declare the getter and setter methods as semi-private
- Write this line:
	- `<attribute_name> = property(<getter_name>, <setter_name>)`

Lets do it step-by-step together here:
Step 1, declare the class and create the constructor:
```python
class ExampleClass:
	def __init__(self):
		pass
```
Step 2, declare the attribute in the constructor:
```python
class ExampleClass:
	def __init__(self, attribute):
		self._attribute = attribute # _ makes it semi private
```
Step 3, declare the getter and setter methods as semi-private:
```python
class ExampleClass:
	def __init__(self, attribute):
		self._attribute = attribute # _ makes it semi private

	def _get_attribute(self): # Getter
		return self._attribute

	def _set_attribute(self, new_value):
		self._attribute = new_value
```
Step 4, write the `property` line:
```python
class ExampleClass:
	def __init__(self, attribute):
		self._attribute = attribute # _ makes it semi private

	def _get_attribute(self): # Getter
		return self._attribute

	def _set_attribute(self, new_value):
		self._attribute = new_value

	attribute = property(_get_attribute, _set_attribute)
```

Now that we have it all done, lets use the Simpler Syntax to call the attribute `attribute`:
```python
obj = ExampleClass(12)
print(obj.attribute)
>>> 12
obj.attribute = 24
print(obj.attribute)
>>> 34
```
> This is great an all, but how do we know we are using the methods and not just accessing the attribute directly?
> Good question, lets add some print statements to the methods to prove that we are using them

Adding print statements to the methods to prove we are using them:
```python
class ExampleClass:
	def __init__(self, attribute):
		self._attribute = attribute # _ makes it semi private

	def _get_attribute(self): # Getter
		print("Getting attribute")
		return self._attribute

	def _set_attribute(self, new_value): # Setter
		print(f"Setting attribute to {new_value}")
		self._attribute = new_value

	attribute = property(_get_attribute, _set_attribute)

obj = ExampleClass(12)
print(obj.attribute)
>>> Getting attribute
>>> 12

obj.attribute = 24
>>> Setting attribute to 24

print(obj.attribute)
>>> Getting attribute
>>> 24
```

## Deleter Methods
To be honest, I'm not sure why the professors went over deleter methods, since we have no use for memory management at this stage in the course, but here we go. Deleter methods are used when you are done with using an attribute, and you want to free up its memory for use later in the program. These are useful for very long and memory intensive programs, not so much here.

Along with getter and setter methods, deleter methods follow the same syntax when making them:
- Write `def`
- Add an `_` so it is semi-private
- Write `del_<attribute_name>`
- Add parentheses
	- Inside the parentheses, add `self`

Lets add a Deleter method to our `ExampleClass` from above for the attribute `attribute`:
```python
class ExampleClass:
	def __init__(self, attribute):
		self._attribute = attribute # _ makes it semi private

	def _get_attribute(self): # Getter
		print("Getting attribute")
		return self._attribute

	def _set_attribute(self, new_value): # Setter
		print(f"Setting attribute to {new_value}")
		self._attribute = new_value

	def _del_attribute(self): # Deleter
		print("Deleting attribute")
		del self.attribute

	attribute = property(_get_attribute, _set_attribute)
```

#### Adding a Deleter Method to the `property`
Just like a getter and setter can be added to the `property` function, a deleter method can be added as well. It is always added at the end of the `property` function. We do this for the same reason we add getters and setters to the property function: to access them using the Simpler Syntax.

The new property function line would look like this:
`<attribute_name> = property(<getter>, <setter>, <deleter>)

## The `@property` Decorator
In Python, the `@property` decorator is used to create "getter" methods for class attributes, allowing you to define custom behavior when getting the value of an attribute. It's another way to make a method appear as an attribute so that you can access it like a regular attribute, rather than as a method call. This can be useful for encapsulation and controlling access to class attributes.

To use the property decorator, follow these steps:
- Add the `@property` decorator
- Declare the function using `def`
- Name the function whatever is the name of the attribute
- Add parentheses and `self` as the parameter
- Add the method body

Here is an example of using the @property decorator:
```python
class MyClass:
	def __init__(self, attribute):
		self.attribute = attribute

	@property
	def attribute(self):
		return self.attribute
```

Now that we have a getter method using the property decorator, we can use similar decorators for the setter and deleter. Instead of `@property`, for the setter it would be `@<attribute>.setter` and for the deleter it would be `@<attribute>.deleter`. 

An example of adding a setter and deleter using decorators:
```python
class MyClass:
	def __init__(self, attribute):
		self.attribute = attribute

	@property
	def attribute(self):
		return self.attribute

	@attribute.setter
	def attribute(self, new_value):
		self.attribute = attribute

	@attribute.deleter
	def attribute(self):
		del self.attribute
```

This does exactly the same thing as the property function that we went over earlier in the note page, the only difference is the syntax. You my prefer to use the property function or the decorator, it doesnt really matter in the grand scheme of things.