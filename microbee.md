---
permalink: /microbee/
title: "Microbee"
layout: post
---

Back in the dim, dark, 1980's,  my family owned a Microbee. 
The Microbee was an Australian designed and manufactured Z80-based home computer.
 
I spent many happy hours messing about with it before time marched on and I moved into the PC world.

But I have always had a soft spot for the 'Bee.

As retrocomputing has become a thing,  I have been mucking around with emulators of older computing platforms.

I only ever found a handful of emulators built for the Microbee and none are targeted at MacOS.

So I decided to roll my own

My implementation is called Abeja ( Spanish for bee )

It is written for MacOS Sonoma using Swift/SwiftUI.

The GitHub repository for Abeja can be found [here](https://github.com/fatherdougalmaguire/Abeja "Abeja GitHub repository")

![My first computer](/assets/images/Microbee32K_IC.png)

### Related posts

<ul>
  {% for post in site.posts %}
      {{ post.date | date: date_format }}
      <br>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
  {% endfor %}
</ul>
