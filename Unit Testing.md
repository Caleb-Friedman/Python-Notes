### What are Unit Tests?
Unit tests are a very standard way of testing any code that you write. It is based around "cases", which attempt to make sure a very small amount of code works perfectly as it is bad practice to try and cover multiple bases in one test. These are programs that automatically run certain inputs through other programs or parts of programs.

They are usually made to run in a few seconds and if written well, they cover close to, if not, all input situations to make sure everything works and intended.

Remember:
- Unit tests focus on testing the least amount of code possible in any one test.
- Each one tests a single unit of the total amount of available code.

### Why use Unit Tests?
According to the slides, there are four main reasons to write unit tests:
- To ensure that code is working the way the *developer thinks it should*  
- To ensure that code *continues working when we make changes*  
- To ensure that the *developer understood the requirements*  
- To ensure that the code we are writing *has a maintainable interface*

A very common practice in the programming world is called "Test Driven Development", in which the unit tests are created before the actual code is create for a feature / system. This makes sure that all tests are completed, as in programmers dont delete failed tests, and this approach forces programmers to acknowledge how the code will be used.

Test driven development breaks down large tasks into much smaller ones,  but when combined, creates the final project all the same. It also tells us how our public interface should look as the entire public interface should be in the tests.

### Using the unittest Library
#### Writing Unit Tests
Since professor Rahman told us during our Wednesday lecture that we will not have to write unit tests for our exam, this section will be pretty light of programming and focus more on theory.

Whenever we want to make our unit tests, we first have to import the unittest module:
```python
import unittest
```

After we have imported unittest, we need to create our test. To do this, we need to create a class and inherit `unittest.TestCase`. Inside of the class, we will create our methods, which will be our test cases:
```python
class TestCases(unittest.TestCase):
	def test_case1(self):
		# Test goes here
	
	def test_case2(self):
		# Other test goes here
```
> Test case methods' names must start with `test_`

To run our tests, we need this piece of code:
```python
if __name__ == "__main__":
	unittest.main()
```
##### Assertion Statements
Here is a list of all of the different assert statements used in Professor Rahman's slides, their corresponding descriptions and an example:
- assertEqual --> Checks if two values are equal
	- Ex: `assertEqual(1, 1)` --> True
	- Ex: `assertEqual(1, 3)` --> False
	- Opposite: assertNotEqual
- assertTrue --> Checks if a thing (variable, condition) is true
	- Ex: `assertTrue(1 == 1)` --> True
	- Ex: `assertTrue(1 == 3)` --> False
	- Opposite: assertFalse
- assertGreater --> Checks if a value is greater than another value
	- Ex: `assertGreater(3, 1)` --> True
	- Ex: `assertGreater(1, 3)` --> False
	- Opposite: assertLess
- assertGreaterEqual --> Checks if a value is greater or equal to another value
	- Ex: `assertGreaterEqual(1, 1)` --> True
	- Ex: `assertGreaterEqual(3, 1)` --> True
	- Ex: `assertGreaterEqual(1, 3)` --> False
	- Opposite: assertLessEqual
- assertRaises --> Checks if a method raises a certain error
	- ```def divide_by(num): 
		   return 5 / num```
	- Ex: `assertRaises(ZeroDivisionError, divide_by, 0)` --> True
- assertIn --> Checks if a value is in a sequence
	- Ex: `assertIn(1, [1, 2, 3])` --> True
	- Ex: `assertIn(1, [4, 5, 6])` --> False
	- Opposite: assertNotIn
- assertIsNone --> Checks if a variable is `None`
	- `var = None`
	- Ex: `assertIsNone(var)` --> True
	- Opposite: assertIsNotNone
- assertSameElements --> Checks if a collection (list, tuple, set, dict) has the same elements of another collection **IGNORING ORDER**
	- Ex: `assertSameElements([1, 2, 3], [1, 3, 2])` --> True
	- Ex: `assertSameElements([1, 2, 3], [1, 3, 4])` --> False
- assertListEqual --> Checks if a list has the same elements **IN THE SAME ORDER** as another list
	- Ex: `assertListEqual([1, 2, 3], [1, 2, 3])` --> True
	- Ex: `assertListEqual([1, 2, 3], [4, 5, 6])` --> False
	- Similar asserts:
		- assertSetEqual
		- assertTupleEqual
		- assertSequenceEqual
		- assertDictEqual

##### setUp and tearDown Methods
Sometimes when you create unit tests, you need code at the start of each test to set up some of the functionality of the test, such as creating variables or objects. Instead of creating these objects inside of every individual case, we can use the setUp method. This method is run before each test case is run, so no need to create these variables in every test case.

The tearDown method is basically the opposite of the setUp method: it runs after each unit test and is used to clean up the variables and objects created before running the other tests.

#### Unit Test Outputs
Whenever you run your unit tests, there will be an output regarding which tests pass and which tests fails. Here is a list of all possible outputs and their corresponding reasons:
- "." --> Test passed
- "F" --> Test failed
- "s" --> Test skipped
- "x" --> Test failed (was an expected failure)
- "u" --> Test passed (was an expected failure)
