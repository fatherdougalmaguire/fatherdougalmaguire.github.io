---
title: Blogging
layout: post
tags:
 - jekyll
 - Github pages
---
I thought it my be a good idea to track the progress of my various software projects.

Mainly as I am notoriously bad at documentation

But also give me a way to track my progress (or lack thereof).
And (maybe) provide something interest to any readers. 

After checking out the various bogging options, I stumbled across [GitHub Pages](https://pages.github.com/)

It ticked a few boxes:

1. It was free
2. It was open source
3. I was intrigued by the ability to use [Jekyll](https://jekyllrb.com/) as the engine to build a website with lots of bells and whistles
4. It was free 

There are a plethora of complex and visuallt appealing themes available ( at all price points ).

A sample of some of these themes can be found at [Jekyllthemes.io](https://jekyllthemes.io)

![Jekyllthemes.io](/assets/images/jekyllthemes.io.jpeg)

I've ended up building this site using the default Jekyll theme [Minima](https://github.com/jekyll/minima)

But I hope to migrate it to something a little more visually stylish as I explore the capabilities of Jeykll and to document my journey.

### Related posts

<ul>
  {% for post in site.posts %}
      {{ post.date | date: date_format }}
      <br>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
  {% endfor %}
</ul>