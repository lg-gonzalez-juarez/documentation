---
title: 00. index
tags: [machinelearning]
keywords: #
#summary: "This is just a sample topic..."
sidebar: mchlrn_sidebar
permalink: mchlrn_00.html
folder: machinelearning
---
This pages shown the fundamentals of python required to take and pass the certified  AWS Certified Machine Learning - Specialty 2020 exam. 
This was extracted from [Linux Academy Course](https://linuxacademy.com/cp/coursescheduler/view/id/492069)
This covers:

<!-- List of all pages with a python tag -->

<ul>
{% assign sorted_pages = site.pages | sort: 'title' %}
{% for page in sorted_pages %}
{% for tag in page.tags %}
{% if tag == "machinelearning" %}
<li><a href="{{ page.url | remove: "/"}}">{{page.title}}</a></li>
{% endif %}
{% endfor %}
{% endfor %}
</ul>


{% include links.html %}