---
title:  "Customer Behavior & JavaScript"
date:   2023-08-01
categories: lewagon
---
We can use JavaScript to modify and interact with elements, based on the elements already created, by using DOM.

DOM (Document Object Model): represents an HTML or XML document as a tree-like structure. The DOM allows programs, such as web browsers, to manipulate and interact with the structure, content, and style of a document.

Select an item : since each HTML element is an object represented in the DOM, we can interact with these objects and manipulate them in JavaScript. To do this, we must select the element with which we want to interact using the following method: document.querySelector(CSS_SELECTOR)

The document here refers to the entire HTML document. The SELECTOR_CSS can be an HTML tag, a class or an id (or a combination of the three to access a specific element).

For example, you can select this list item:

ul id="players" ul =JS code ==> querySelector("#players")

Note that :
- The # sign used in ("#players"): To find the right element in the DOM, you need to be specific when telling JavaScript what to look for. When assigning variables in JavaScript, you must first include a special keyword, in this case const.
- Once you have selected your element and stored it in a variable, check that you have found the correct elementn (forgot the # while searching for the element with id="players", or you may have a typo or any other error ?) : to find out is to display, or print, and check.

In JavaScript, to print we use a method called console.log(). This method takes an argument, which corresponds to what we want to display. Let's see some examples:

// print the "Hello world" string:
console.log("Hello world")
// => "Hello world"

// print the value of a selected variable:
const list = document. querySelector("#players")
console.log(list)
// => ul id="players" ul

Modify an element : once we have selected the element with document.querySelector and stored it in a variable, we can start having fun interacting with it :

- change the text with innerText : const slogan = document.querySelector(".motto")slogan.innerText = "Change your life, learn to code"
- change a CSS class with classList : this way we can add or remove a class. Ex: button class="btn btn-primary" id="my-button" Clique sur moi /button.To hide it so that users cannot click on it : first, we define in our CSS a class called d-none, which will hide the element to which it is applied:
.d-none {
display: none;
}

To add this CSS class to our button, we must first select it in the DOM:
- const button = document. querySelector("#my-button")
Then, we can modify its classes, like this:
- button.classList.add("d-none")button.classList.remove   ("d-none")


Event is a specific action that should trigger another action. We use addEventListener, 3 parties:

- element on which we want to listen to a specific event
- type of event you want to listen to
- code that we want to execute when the event occurs.

Ex: example with a button:

button class="btn btn-primary" id="my-button">Click me/button

When the user clicks on the button, we want to deactivate it (disable):

 // first we select the element:
const button = document. querySelector("#my-button")

// then, we listen to the moment when the user clicks on the button:
button. addEventListener ("click", () => )
// on click, this code will be executed:
button.disabled=true
