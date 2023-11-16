## Using Built-in Classes
In python, there are multiple different built-in classes, otherwise known as built-in types. Some of these types we have already learned in COP 2512, such as lists, sets, tuples and the one which will probably be on the exam: dictionaries. For the examples here, we will be inheriting the dictionary type.

Have you ever wanted custom methods inside of a dictionary? Well, you probably didnt, but now you can! By creating a new class and inheriting the built-in `dict` class, we can create custom classes that act like dictionaries, but can contain methods that we build.

For this example, lets make a class that inherits the dictionary type like this:
```python
class NewDictionary(dict):
	pass
```

We can create objects of out new class, and add key/value pairs to the objects just as we would a normal dictionary. Lets make a `car` dictionary with three key/value pairs:
```python
car = NewDictionary()

car["company"] = "Ford"
car["model"] = "F-150"
car["year"] = "2022"

print(car)
>>> {'company': 'Ford', 'model': 'F-150', 'year': '2022'}
```

Now lets add a method to this class, this method will loop through all of the keys in the dictionary and compare their lengths. It will find the **key** with the shortest length, and print the key/value pair:
```python
class NewDictionary(dict):
	def find_shortest(self):
		baseline = None 
			#loops through itself and i equals each key. On the first loop I would equal the zeroth key and so on
		for i in self: 
			if baseline == None or len(baseline) > len(i):
				baseline = i
		return i, self[i]

car = NewDictionary()

car["company"] = "Ford"
car["model"] = "F-150"
car["year"] = "2022"

print(car.find_shortest())
>>> ('year', '2022')
```

## Special Python Methods
Python has some special methods that can be added to you classes. These special methods a special syntax, they all have two underscores before and after the method name, for example: \_\_init\_\_  and \_\_str\_\_. 

In this note page, we will be polymorphing the special python methods to do what we want them to do. A strong grasp of the Polymorphism and Inheritance note pages will be critical to understanding this.
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

### The `__len__` Method
We have used the len() method many times before in both this course and in COP 2512 course last semester. When used on a list or string, the len() function gives us back how many values are in the list or how many characters are in the string. Whenever we make our own list-type class by extending `list`, we can polymorph the \_\_len\_\_ method to return something else instead. Even in classes that dont extend built in types, we could create a \_\_len\_\_ method to do stuff.

Why would you ever do this? Who knows, but we can!

Here is an example of polymorphing the \_\_len\_\_ function:
```python
class NewList(list):
	def __len__(self):
		print("Returning the length of the list")
		return super().__len__()

x = NewList()
x.append(1)
x.append(2)

print(len(x))
>>> Returning the length of the list
>>> 2
```
> Here we basically keep the functionality of the original len() function by calling super() on it, and we add a little functionality by adding a print statement

### The `__reversed__` Method
Another method that built-in types usually have is the \_\_reversed\_\_ method, which returns the items in that type in reversed order. For example:
```python
x = list()
x.append(1)
x.append(2)
x.append(3)

for item in reversed(x):
    print(item, end=' ')
>>> 3 2 1 
```
> Since x is a list, reversed(x) would be a <list_reversediterator> type. Why doesnt it return a list?
> Because python sucks thats why.

Because reversed() doesnt return a list, we cant print it like normally which is quite lame. Instead we need the for loop like we did above. If you want the reversed() method to return the corresponding type whenever we call it on our own type that inherits a list, we could polymorph the \_\_reversed\_\_ function like this:
```python
class NewList(list):
	def __reversed__(self):
		new = NewList() 
		for i in self:
			new.insert(0, i)
		return new

x = NewList()
x.append(1)
x.append(2)
x.append(3)

print(reversed(x))
>>> [3, 2, 1] 
print(type(reversed(x)))
>>> <class '__main__.NewList'>
```
> The `.insert(0, i)` puts the value `i` into index `0` in the list.

> Now the reversed returns the value in our NewList type rather than a list_reversediterator type.

### The `__getitem__` Method
I doubt that you have seen the getitem() method before, but it has been working in the background like every time you have worked with lists or string splicing before. Whenever you use this syntax: `list_name[index]` it calls the list object's getitem() method. 

Lets test that:
```python
x = list()
x.append(1)
x.append(2)

print(x[0])
>>> 1
print(x.__getitem__(0))
>>> 1
```

Have you ever wanted to print something other than the value associated with the index whenever you used the `list_name[index]` line? No? Yeah I thought so. But we can print other things when that happens by polymorphing the getitem() method.

Here is an example where we print "Item: " before the item associated at the specified index:
```python
class NewList(list):
    def __getitem__(self, index):
        return f"Item: {super().__getitem__(index)}" 

x = NewList()
x.append(1)
x.append(2)
x.append(3)

print(x[0])
>>> Item: 1
```
> We call the super().\_\_getitem\_\_(index) to actually retrieve the item within the list, and add it to the fstring

### The `enumerate()` Function
Woah, Taseef is teaching something actually useful when coding in python regularly?? This is cause for celebration! Yeah you heard that right, the enumerate() function is actually really useful when looping through lists, and especially dictionary types.

All that praise, but what does it actually do? Essentially, it takes a list, and returns a list of tuple which contain each index and its corresponding elements. Remember a tuple is just a list whose objects cannot be changed.

I know that sounded complicated, perhaps an example will be better in understanding it:
```python
x = list()
x.append("Kane")
x.append("Jade")
x.append("Soloman")

for item enumerate(x):
	print(item)
	
>>> (0, 'Kane')
>>> (1, 'Jade')
>>> (2, 'Soloman')
```
> Similar to when we were using the reversed() function, we cannot just print enumerate(x) since it is not technically a list, it is an `enumerate` type object. So just use a for loop to print out each pair.

