---
title: More info about Friday Theme
description: 
published: true
date: 2022-03-01T18:44:35.101Z
tags: 
editor: markdown
dateCreated: 2022-03-01T18:44:32.057Z
---

## What is it?

{% include components/intro.md %}

## Full Feature List

- Installation
  - Designed for Jekyll 3.8
  - Compatible with GitHub Pages
- Configuration
  - Useful data files to quickly generate the profile sidebar and site navigation
  - Easy to configure, minimal options, sensible defaults
- Styling
  - Styled with Bootstrap, proven to work cross-platform
  - Minimal additional SCSS to get in the way
  - Entirely customisable by tweaking the Boostrap SCSS variables
- Layout
  - 2 column layout
  - Context-sensitive sidebars for blogs, documentation pages and normal content
  - Narrow/wide page options
  - Responsive layout built in
  - Lots of helpful includes and components to build out your site
- JavaScript and Components
  - jQuery and Bootstrap JS included
  - Use all the Bootstrap components
- Other goodies
  - Entypo SVG icons included
  - Syntax highlighting for code fragments using Rougify for over 100 different languages
- Blog
  - A collection layout to build a blog with full support for tagging
  - Interactive tag filtering for the blog
- Projects
  - A layout to list your projects, with a documentation-like layout for each project
  - Table of contents generation for documentation pages
- Permalinks
  - Permalinks using baseurl throughout for deployment under a subdir or on GitHub pages
  - Permalinks using .html throughout for deployment to environments not using default directory indexes

## Examples

Here's some quick examples of what it can do.

### Code Highlighting

{% highlight javascript %}
var modulePattern = (function() {
    // your module code goes here
    var sum = 0 ;

    return {
        add:function() {
            sum = sum + 1;
            return sum;
        },
        reset:function() {
            return sum = 0;
        }
    }
}());
{% endhighlight %}

### Bootstrap Components

Here's a CSS component, it's an alert box with the info color:

<div class="alert alert-info">
    A simple info alert!
</div>

And this is a more sophisticated example, using the JS to include a carousel of images:

<div id="carouselExampleControls" class="carousel slide mb-4" data-ride="carousel">
    <div class="carousel-inner">
        {% for img in page.images %}
            <div class="carousel-item {% if forloop.first %}active{% endif %}">
                <img src="{{ img }}" class="d-block w-100" alt="">
            </div>
        {% endfor %}
    </div>
    <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
    </a>
</div>

The spinner.

<div class="spinner-border text-dark mb-4" role="status">
  <span class="sr-only">Loading...</span>
</div>

### Icons

There's a suite of hundreds of Entypo icons included, here's just a few.

<div class="d-flex align-items-center mb-4">
    <span class="icon grey mr-2">
        {% include entypo/clock.svg %}
    </span>
    <span class="icon grey mr-2">
        {% include entypo/cycle.svg %}
    </span>
    <span class="icon grey mr-2">
        {% include entypo/chevron-up.svg %}
    </span>
    <span class="icon grey mr-2">
        {% include entypo/new-message.svg %}
    </span>
    <span class="icon grey mr-2">
        {% include entypo/shopping-cart.svg %}
    </span>
</div>


