---
title: Python_intro
tags: [python]
keywords: trainning, courses
last_updated: January 3th, 2021
summary: "This shows a review of mainly courses that I have considered"
sidebar: mydoc_sidebar
permalink: python_00.html
toc: false
folder: python
---

<div class="row">
         <div class="col-lg-12">
             <h2 class="page-header">Python Course</h2>
         </div>
         <div class="col-md-3 col-sm-6">
             <div class="panel panel-default text-center">
                 <div class="panel-heading"></div>
                 <div class="panel-body">
                     <h4>Python1</h4>
                     <p>Fundamentals.</p>
                     <a href="https://www.coursera.org/" class="btn btn-primary">Learn More</a>
                 </div>
             </div>
         </div>
         <div class="col-md-3 col-sm-6">
             <div class="panel panel-default text-center">
                 <div class="panel-heading"></div>
                 <div class="panel-body">
                     <h4>Python 2</h4>
                     <p>Here 2.</p>
                     <a href="tag_navigation.html" class="btn btn-primary">Learn More</a>
                 </div>
             </div>
         </div>
         <div class="col-md-3 col-sm-6">
             <div class="panel panel-default text-center">
                 <div class="panel-heading"></div>
                 <div class="panel-body">
                     <h4>Python 3</h4>
                     <p>Text.</p>
                     <a href="tag_single_sourcing.html" class="btn btn-primary">Learn More</a>
                 </div>
             </div>
         </div>
         <div class="col-md-3 col-sm-6">
             <div class="panel panel-default text-center">
                 <div class="panel-heading"></div>
                 <div class="panel-body">
                     <h4>Python 4</h4>
                     <p>Text.</p>
                     <a href="tag_formatting.html" class="btn btn-primary">Learn More</a>
                 </div>
             </div>
         </div>
</div>


## Generating a list of all pages with a certain tag

<ul>
{% assign sorted_pages = site.pages | sort: 'title' %}
{% for page in sorted_pages %}
{% for tag in page.tags %}
{% if tag == "python" %}
<li><a href="{{ page.url | remove: "/"}}">{{page.title}}</a></li>
{% endif %}
{% endfor %}
{% endfor %}
</ul>

{% include links.html %}
