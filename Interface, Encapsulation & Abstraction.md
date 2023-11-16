### These are essentially the practice of hiding the inner workings of code and classes to be more user friendly.

## Interface
Classes should not be able to access the inner working of other classes, an example of this in life would be a person not knowing the inner circuitry of a television, and instead communicating with the television using a remote control.

There are two types of interfaces:
- Public interface
- Private interface

### Public Interfaces
A public interface is an interface that allows for objects outside of the class to use the class’s methods and attributes. For example, a remote control has a public interface which are the remote’s buttons and controls. The person operating the remote control can communicate with the remote control by pressing its buttons. If you take away only one thing from this, Public interfaces are able to be accessed from outside the class.

### Private Interfaces
As you may have guessed, private interfaces are only allowed to be accessed from inside its own class. Private methods and attributes should not be accessed from outside its own class, but are needed for the class to work. To continue with our remote control example, the frequency of the waves that allow the remote to communicate with the TV should be private, since the user should not change these.

### Encapsulation
Encapsulation is the practice of actually hiding things from the user in regards to the inner working of classes. The most common example of this would be getter and setter methods in classes.

This is generally referred to as `Information hiding` and these two are often used interchangeably, but this is not always the case. An attribute may be encapsulated with getter and setter methods, but these are not always hidden from the user.
[Encapsulation in Python](https://www.notion.so/Encapsulation-in-Python-48d26614d51d40c592d89311f688570f?pvs=21)

### Abstraction
Abstraction is the concept of generalization. You dont need to know how the different pieces of a computer work when you turn it on to play some video games, all you need to know is how to press the power button.

In Object Oriented Programming, abstraction allows us to obscure the inner workings of a class by using methods and attributes inside of the classes. For example, if we had a Computer class, we could have a method called PowerOn() that the user calls whenever they want to turn on the computer. The user has no need to know the inner code of the method, all they need to know is the outcome.