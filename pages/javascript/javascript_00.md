---
title: javascript 0
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: javascript_sidebar
permalink: javascript_00.html
folder: javascript
---
# Introduction to JavaScript

## Introduction

### Welcome to this course 
by Michael McClaren

This is a text test

### Prerequisites

- basic skills

## The History of JavaScript

### Implementing Client-Side Scripting

Hypertext is a way to link and access information of various kinds as a web of nodes in which the user can browse at will. It provides a simple user-interface to large classes of information (reports, notes, data-bases, computer documentation and on-line help)

In this lesson we will look back at the history of the internet and the creation of the World Wide Web. We will see how the internet used to be a very dull and boring place filled with a lot of static web pages. This leads us to the reason that client-side scripting was implemented. Once we see where we came from, compared to where we are now, we can understand the need for JavaScript.

#### The challenge of dynamic content
The problem was that the network speeds that were available made it difficult to load elements.

Photos and graphics were especially troublesome.

Page events such as mouse-over and on-click required the whole page to be reloaded.

This was slow and pages were not responsive.

Netscape navigator was the first browser to implement client-side scripting via the scheme script language. This would later become JavaScript. Others would follow, and eventually all modern browsers would support JavaScript as we know it today.

Javascript on the client allows just in time compilation of the code, to permit manipulation of the HTML elements in a page without requiring reloads of the full page.

## Creating a Modern and Dynamic Internet

In this lesson we will look at synchronous and asynchronous update methods, and how asynchronous JavaScript and XML AJAX is used to speed up the load times of web pages. The concept of asynchronous loading becomes fundamental in creating dynamic and responsive web pages. Once we understand these ideas we can move forward with creating awesome dynamic content, or maybe just a place to store photos of cats. That is what the internet is used for right?

updating pages dynamically requires standards for describing data and objects.

### Describing Data

- JavaScript Object Notation (JSON)
- eXtensible Markup language (XML)

## Syncrhronous Updates

When a request is made, the requestor waits until the request is processed and a response is given before it can continue.

## Asynchronous updates

When a request is made, the requestor does not wait but loads the pages and update when the data is returned

# Client-Side Scripting Basics

## Exploring the Document Object Model (DOM)

In this lesson we will be building on what we learned about how internet web pages are created. We will be looking at the structure of Hypertext Markup Language (HTML) and see how HTML elements are nested in web pages. We will also briefly talk about styling HTML elements to get a handle on how they are displayed.

All code in these lessons can be created in the text editor of your choice, and then opened using the file:// prefix in your browser.

This is the HTML that is used in this lesson.

We start out with this:

```
<hmtl>
    <head>
        <h1>This is some text</h1>
    </head>
    <body>
        <p>This is a paragraph</p>
        <p>This is a second paragraph</p>
    </body>
</hmtl>
```

We end with this:

```
<hmtl>
    <head>
        <h1 style="text-align:center;">This is some text</h1>
    </head>
    <body>
        <p style="text-align:center;">This is a paragraph</br>
        This is a second paragraph add some more text</p>
    </body>
</hmtl>
```

## Understanding JavaScript Syntax (Hello World)

In this lesson we will be working with the template from the previous lesson, and creating some dynamic elements. In this process we want to ensure that we understand the concept of ```syntax``` as it relates to JavaScript. Since this is an introduction to JavaScript, we will not be getting too caught up in the syntax. But we want to be aware of it and ensure that we are writing our code correctly.

The web browser used in this lesson is FireFox, and the Integrated Developer Environment is Visual Studio Code with only the default installation. All code in these lessons can be created in the text editor of your choice, and then opened using the file:// prefix in your browser.

Here is the final code that was used in this lesson. See if you can figure out the mistake.

```
<hmtl>
    <head>
        <h1>This is some text</h1>
    </head>
    <body>
        <p id='p1'>This is a paragraph</p>
        <p id='p2'>This is a second paragraph</p>
        <button type='button' 
        onclick="document.getElementById('p1').innerHTML='Hello World!';">
        hello</button>
        <button type='button' 
        onclick="document.getElementById('p2').innerHTML='This is JavaScript.';">
        JavaScript</button>
    </body>
</hmtl>
```

### Sintax highlights

Sintax refers to rules that define a correctly structured program

- Case sensitive .log() is not the same as .Log()
- Semicolon (;) line endings Java codes goes here;
- Comments //single line comment

[link video](https://linuxacademy.com/cp/courses/lesson/course/7548/lesson/2/module/686)

### Working with Image Tags (Cats and Dogs)

In this lesson we will be taking what we have learned about the Document Object Model (DOM) and use that to put the real power of the internet to work! We will be leveraging the power of JavaScript to display pictures of pets. I do not want to take a side, so we will be switching between a photo of a cat and a photo of a dog. This will show how media can be manipulated with JavaScript by leveraging the src property of an HTML element.

Git repo for this lesson:

´´´
https://github.com/linuxacademy/content-introduction-to-javaScript
´´´

[video link][https://linuxacademy.com/cp/courses/lesson/course/7548/lesson/3/module/686]

# More Advanced Client-Side Scripting

## Using Variables and Arrays

In this lesson we will look at variables and arrays. We will see that varaibles are place holders for values, and the place holders sometimes make it easier to work with the value that they represent. We will also see that an array is a special type of variable that is used to group objects logically in one place. We will introduce the concept of the ```zero index```, which means that items are counted starting at 0. This is a bit strange at first, but it is something that is present in almost all programming languages.

[link video](https://linuxacademy.com/cp/courses/lesson/course/7549/lesson/1/module/686)

## Working with Conditionals and Looping

In this lesson we will be looking at adding some decision making to our programs using conditionals with the if statement. We will also use what we know about arrays to make use of looping with for. This will allow us to access all of the items in the array so that we can disaply the data on the page. We are just skimming the surface of these knowledge areas, but we need to be familiar with them so that as we move forward we understand the terms that are fundamental to programming.

Code used in the conditionals example:

```
<html>
    <head>

    </head>
    <body>
        <p id = 'p1'>value not set </p>
        <script>
            var value = 4;
            if(value < 5)
            {
                document.getElementById('p1').innerHTML = value;
            }


        </script>

    </body>
</html>
```
Code used in the looping example:

```
<html>
    <head>

    </head>
    <body>
        <p id = "p1">value no set</p>
        <script>
            var array = ["one","two","three","four"];
            var output = "";
            for(i = 0; i < array.length; i++){
                output += "This is item " + array[i] + "</br>" ;
            }
            document.getElementById('p1').innerHTML = output;
        </script>

    </body>
</html>
```

[link video](https://linuxacademy.com/cp/courses/lesson/course/7549/lesson/2/module/686)

## Understanding the Basics of Functions

In this lesson we will learn about the structure of a function. We will see some practical examples of functions, and see how they can be applied to create an interactive web page. These are just the basics of functions, and this lessons will be a building block as you progress in your journey.

[link video](https://linuxacademy.com/cp/courses/lesson/course/7549/lesson/3/module/686)

A function is a named reusable block of code that begins with thr function keyowrd

- function key word
- name of the funcion
- arguments 
- return key word (optional)
- value that gets returned (optional)

## Introducing JavaScript Frameworks

In this lesson we will see how to use an external source for JavaScript in our pages. We will look at libraries and convert one of our projects so that it uses an external library as its JavaScript source.

We will then quickly look at some of the more popular JavaScript libraries and frameworks that you may want to use for your projects.

# Server-Side Basics

## Exploring Server-Side JavaScript with NodeJS

[video link](https://linuxacademy.com/cp/courses/lesson/course/7550/lesson/1/module/686)

In this lesson we will be using NodeJS to create a web server that can handle a basic request. This is one of the simplest implementations of Java Script on the server.

Some of the reasons that we might want to implement server-side JavaScript is so that we can handle both sides of the transaction using one language. Also, server-side technologies are the other half of the equation when we think about how we access and serve persistent data on the internet. While client-side JavaScript is concerned with how the data is displayed, server-side JavaScript an concern itself with how that data is manipulated and stored.

## Resources for this lesson:

### Node Installer

```
URI : https://github.com/nodesource/distributions/blob/master/README.md#rpminstall

curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -

sudo yum install -y  nodejs

node -v
```

Simple Node HTTP server ( index.js )

```
var http = require('http');

http.createServer (function(req, res)
{
    res.write('Hello World');
    res.end();
}).listen(8080);
```

## Introducing REST and APIs

[video link](https://linuxacademy.com/cp/courses/lesson/course/7550/lesson/2/module/686)

In this lesson we will be looking at how web applications are built using REpresentational State Transfer (REST). We will explore the guidelines that describe REST architecture, and try to understand how they allow the internet to be responsive and uniform. We will talk about Application Programming Interfaces (API)s and see some real world examples of APIs in action.

This is intended to be just a peek into these topics. There are many wonderful explorations of these topics to be found, and in the end I really want to encourage you to learn more about them.