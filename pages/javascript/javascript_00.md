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

