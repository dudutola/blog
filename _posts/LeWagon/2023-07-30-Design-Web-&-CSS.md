---
title:  "Design Web & CSS"
date:   2023-07-30
categories: lewagon
---
Design Web involves creating visually appealing and user-friendly layouts for websites.

CSS (Cascading Style Sheets) is a programming language used to describe the presentation and styling of HTML documents. It provides a wide range of styling options to control the appearance of web pages, like the color, font form, size, spacing, create columns or add animations.

To write our CSS code, we must have a file named style.css. And to work with index.html file, we have to put the link in the head tag, this way :
   - head (autres metas) link href="style.css" rel="stylesheet"head. Then, they can work together.

CSS is used to add a style. The generic version of the syntax is as follows:
- element { propriete: valeur; }
To add colors the best way is to use the exactly HEX of the colors, because some pc could not recognize words in english. To do that, use sites like : Color Hunt or Coolors, easy way to copy them quickly, in front of the number always add an "#".

For the font family use Google Fonts, copy the link and past this way in the head : link href="https://fonts.googleapis.com/css?family=Chivo:700|Overpass:400,700&display=swap" rel="stylesheet"
(by default = Courier New, Overpass, Chivo).

To change :

- the weight use : font-weight : lighter/bold;
- decoration : text-decoration : none; = used to remove the default underline from links.
- alignment : text-align : center/right;


It's common to apply a different style to an element when it's hovered over. In this case, we are not just talking about a specific element, but rather the specific state of a specific element. To target different states of an element in our CSS, there are so-called pseudo-classes. To add effects when hovering over an element, we use the :hover pseudo-class, like this:
- a {
color: blue;
transition: 0.3s;
}

- a:hover {
color: red;
}

In this scenario, all links in their normal state are therefore blue. But when hovered over, they turn red, with a slight transition when changing color.
Box model used when we have content that we want to group on our web page. We can structure our content like this by adding “boxes” around it, then applying style to them. In HTML, you can do this with the div element (for div-ision).

To apply a style to a div, you have to structure its content and customize its spacing. There are many CSS properties for customizing divs : width, height, padding, margin. To summarize, we can visualize the following div and the corresponding CSS properties:

div {
width: 500px;
height: 350px;
margin: 0 auto;
padding: 15px;
background: white;
box-shadow: 0 0 16px rgba(0,0,0,0.1);
border: 1px solid #F7F7F7;
border-radius: 4px ; (soften or round the edges of the div)
}

ID and Class :
- Id is used to specify a unique element on the page. Then,to target this CSS selector in order to apply a style to it, we use the <strong>#</strong> sign and the name of the id.
- Class is used for recurring elements on the page. We can use it for one element too. To target this CSS selector in order to style it, we use the sign *.* and class name.
