---
title: Blogging
layout: post
include_search : true
excerpt : I thought it my be a good idea to track the progress of my various software projects.
---
I thought it my be a good idea to track the progress of my various software projects.

Mainly as I am notoriously bad at documentation

But also give me a way to track my progress.  
Or lack thereof.   

I had thought of using a[Google Sites](https://sitdes.google.com/)( as it already came with Google Workspace ) but I found the limitations of a turnkey solution a little frustrating.

After checking out the various bogging options available ( and being a little frustrated by the limitations of the turnkey options such as [Google Sites](https://sitdes.google.com/) I stumbled across [GitHub Pages.](https://pages.github.com/)

Not withstanding the fact that it is free, I was intrigued by the ability to use [Jekyll](https://jekyllrb.com/), an open source static site generator created especially with blogging in mind.  

There is a large developer community that has built some very visually appealing templates or "themes" on top of Jekyll.
<br>  
Samples of these can be found at [Jekyllthemes.io](https://jekyllthemes.io)

![Jekyllthemes.io](/assets/images/jekyllthemes.jpg)

### Related posts

<ul class="post-list">
{% assign microbee_posts = site.categories["blogging"] | sort: 'date' %}
{% for post in microbee_posts %}
    {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      {{ post.date | date: date_format }}
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      {{ post.excerpt }}
      <hr>
    {% endfor %}
</ul>
 