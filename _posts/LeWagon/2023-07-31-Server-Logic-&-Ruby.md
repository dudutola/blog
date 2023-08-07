---
title:  "Server Logic & RUBY"
date:   2023-07-31
categories: lewagon
---
Now let's talk about the back-end.

Comment : is always marked with a #. Anything after the # will be ignored by the program.

Puts : to display a message in the console (for example “Hello world!”), we use the Ruby puts keyword. But do not forget to use double quotes (") or single quotes (') around your message, otherwise Ruby will not be able to execute this message.

Data Types : in programming, we mainly write programs to analyze and manipulate data. Without information, the computer would have nothing to do! Let's explore the first three data types in Ruby:

Numeric: all digits and numbers. More specifically, Ruby has:
  - Integerfor whole numbers, both positive and negative.Ex : age = 25
  - Floatfor decimals. Ex: pi = (3.14)

String: represent a sequence of characters enclosed in single or double quotes. For ex:  "Learning to code is fun!"

Boolean: either true (true) or false (false).

Be careful not to use quotes ('or ") with booleans, otherwise Ruby will think it's a String rather than a true or false value.


Variables: the variable is one of the building blocks of all programming languages. It allows us to store our data by giving it a label or a name. We then retrieve its data by calling it by name.To declare a variable in Ruby :  type the name of the variable you want to declare, then the equal sign (=) to assign it a value, like this : my_age = 25. The variable names are written in lowercase, with underscores ( _ ) to represent spaces between words. And if you want to change the value : retype the variable name and the equals sign (=), then the new value: my_age = 26.

Math : it can perform mathematical calculations. 4 simple operators available :

- Addition ( + )
- Substraction ( -)
- Multiplication ( * )
- Division ( / )


To organize and store groups of data, is called a data structure. In Ruby, we have two built-in data structures: the Array and the Hash (unordered collection of key-value pairs, enclosed in curly braces).

Arrays : ordered collection of elements, enclosed in square brackets( [ ] ). Elements can be of any data type. Between the brackets, you can store as much data as you want, separated by commas (,), like this: burger = ["bread", "steak", "salad", "tomato"] In this example, we define a variable called burger, in which we store an array containing four values(ingredients), which are all strings.However, the values inside an array are not necessarily of the same type: an array can contain numbers and any other type of data!

Objects :  tell yourself that any "thing" in Ruby is more than it seems. The number 10 is more than just a number; it is an object on which you can do a lot of interesting things, such as adding, multiplying or even asking questions. Ruby gives all objects a set of built-in methods, which allow us to perform actions, retrieve information, or ask true/false questions about our data. For ex, all objects have a built-in .class method, which tells us the type of the object it is being called on. Methods are called on data using a dot ( . ) and their name, like this:
name = "Dimitri"
name.class

Interact with objects : some built-in methods can be called on all objects (like the .class method), most of the time the built-in methods are specific to the data type. For example, a method that performs a division makes sense for a Float, but not for a String.

If/Else : to modify the flow, we use booleans. Don't forget that a Boolean can only be true or false (no quotes here!).
These booleans are like on-off switches where true is on and false is off. By adding these on-off switches to our code, we define conditions to determine whether a piece of code should be executed or not. Example :
number = 12
if number > 10
puts "The number is greater than 10"
end
 called a conditional statement, or more commonly an if statement = if (the condition is true) then this code is execut, end

We can also declare the other branch of the conditional declaration, i.e. when the declaration is not true, or true, by adding an else to our code, like this:
number = 8
if number > 10
puts "The number is greater than 10"
else
puts "Number is less than 10"
end
“if the number is greater than 10, print this sentence, otherwise print this other sentence”. Since the number 8 is not greater than 10, only the code in the else statement will be executed.By using if/else statements in our code, we can start creating much more complicated and interesting programs!
Methods : allow us to store blocks of code that we will reuse. To define a method, we use the special keyword deffollowed by the name of the method. If we need dynamic information, we can pass parameters to the method:
def say_hi(name)
return "Hi #{name}!"
end

To use this method, we call it with arguments:
puts say_hi("Mary") # => "Hi Mary!"
puts say_hi("John") # => "Hi John!"
