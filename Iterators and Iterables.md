Y'know, this lecture kind of felt like back in year 2 chemistry being told to forget a bunch of things from year 1 chemistry since those were all just oversimplifications. We thought we knew how for loops worked, but now since we are really getting into the nitty gritty, it turns out we have no idea what those things really are.

Back in python 1, we learned the basics of how a for loop worked: it takes a list or another *iterable* data type and takes one element of the data type as the *iterator* per loop. Seemed simple back then, oh how things change.
```python
for i in [1, 2, 3]:
	print(i)
>>> 1
>>> 2
>>> 3
```

## Creating Custom Iterable Types
Back in python 1, we learned that iterability was just a property that some data types had. We could use this property to manipulate individual values in the data type one at a time with a for loop. Now, we can make our own iterable types by giving our class two special python methods: \_\_next\_\_ and \_\_iter\_\_.

So what exactly is an iterable type? Essentially, an iterable type is any data type that we can traverse using a for loop. It is usually a data type that can contain multiple values which can be manipulated and used throughout the program. 

Now, we must make a distinction between iterator and iterables. This is kind of like the Rectangle-Square conundrum, all Squares are Rectangles but not all Rectangles are Squares. All iterators are iterables but not all iterables are iterators. All iterables have a \_\_iter\_\_ method, but only non-iterators allow for all values to be accessed at any time. You can access any value in a list at any time using this syntax: `list[index]`, but in iterators, you can only access the variables using a loop.

Now that we have a rough idea on what iterators are, lets make our own:
- Step 1: Create the class 
```python
class CustomIterator:
	pass
```
- Step 2: Create the \_\_init\_\_, \_\_iter\_\_ and \_\_next\_\_ methods
```python
class IterableNumber
	def __init__(self):
		pass
	
	def __iter__(self):
		return self
	
	def __next__(self):
		pass
```
- Step 3: Implement the functionality for the \_\_init\_\_ and \_\_next\_\_ methods:
```python
class IterableNumber:
    def __init__(self, number):
        self.number = str(number)
        self._index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self._index == len(self.number):
            raise StopIteration

        num = int(self.number[self._index])
        self._index += 1
        return num
```
> This is the barebones implementation for the \_\_next\_\_ and \_\_init\_\_ methods, you can make them as complicated as you need.

I know we just went over a lot and you might not understand everything completely, dont worry, we will go over all of it now.

### Advanced For Loops
Now when I say advanced for loops I dont mean that for loops have extra functionality and more syntax that we are now going to learn, I mean we are going into the nitty-gritty on how for loops work. Back in python 1 we learned that these two loops are equivalent:
```python
i = 0
while i < 4:
	print(i)
	i += 1

for i in range(4):
	print(i)
```

While these loops may have the same output, this is not exactly the true way to make a while loop act exactly like a while loop. If you wanted to make a while loop act EXACTLY like a for loop, it would look something like this:
```python
iterable = iter(range(4))
while True:
	try:
		i = next(iterable)
		print(i)
	except StopIteration:
		break
```
> Hold on there Caleb, what is iter()? what is next()? what is StopIteration? I've seen you use these before but what do they do?
> Good question, lets answer it.

Lets start at the top of the code with the `iterable = iter(range(4))` line. The range() function creates a tuple (an unchanging list) of all the numbers between zero and ten: `(1, 2, 3, 4)`. This will be the iterable object that we will iterate over. Well not exactly, while range() returns an iterable object, it is not an iterator. To make it an iterator, we pass it through the iter() function.

Now we create our while loop to run forever, since True will never equal False. Inside of the loop we have a try / except statement, lets focus on the try for now. So we all know what print does hopefully, but what about next? Next is a function that calls the \_\_next\_\_ method on the object. In all of the basic iterable types in python (list, dict, tuple, etc) have a very similar \_\_next\_\_ method: it keeps track of how many times it has been called, and returns the item at the current index. When the method is called for the first time, it returns the value at index zero, on the next call it returns the value at index one and so on.

What happens when you call the \_\_next\_\_ method and but there are no more indexes in the list? Then it returns a StopIteration error. This is the error we catch in the Except statement that breaks the forever while loop.

Now does the IterableNumber make more sense now? It has a next method that returns the value at the current index and increases the index if the list can keep going, if not it raises a StopIteration error to break the loop.
```python
class IterableNumber:
    def __init__(self, number):
        self.number = str(number)
        self._index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self._index == len(self.number):
            raise StopIteration

        num = int(self.number[self._index])
        self._index += 1
        return num

number = IterableNumber(975)
for i in number:
	print(i)
>>> 9
>>> 7
>>> 5
```

Now lets try it with both the for-like while loop and the for loop:
```python
number = IterableNumber(975)
for i in number:
    print(i)
    
while True:
    try:
        i = next(number)
        print(i)
    except StopIteration:
        break
>>> 9
>>> 7
>>> 5
```
> Huh??? Why did it only print once?? I looped over it two times??
> Well, the index is never set back to zero after the loop ends....

So if we want to reset the index after we hit the StopIteration part, add this like of code `self._index = 0` right above the `raise StopIteration` like this:
```python
class IterableNumber:
    def __init__(self, number):
        self.number = str(number)
        self._index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self._index == len(self.number):
			""" Right Here """
			self._index = 0
            raise StopIteration

        num = int(self.number[self._index])
        self._index += 1
        return num
```

Okay, now it should print twice:
```python
number = IterableNumber(975)
for i in number:
    print(i)
    
while True:
    try:
        i = next(number)
        print(i)
    except StopIteration:
        break

>>> 9
>>> 7
>>> 5
>>> 9
>>> 7
>>> 5
```