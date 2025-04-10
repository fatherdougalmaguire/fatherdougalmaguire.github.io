---
permalink: /microbee/
title: "Microbee"
layout: post
---

![My first computer](/assets/images/Microbee32K_IC.png)
Photo credit : [Wikipedia](https://en.wikipedia.org/wiki/MicroBee "Wikipedia")

<br>
Back in distant past,  my family owned a Microbee. 

The Microbee was an Australian designed and manufactured home computer ( by a company called Applied Technology ), popular during the 1980's.  

It sold particularly well in the educational market.

Initially supplied as a kit ( and later as fully assembled models ),  it driven by a Z80 CPU and came with a relatively generous 16 or 32 Kb of ram.

BASIC was installed in ROM and used audio cassettes to store programs and data. 

Later models included floppy disk drives as well as upgrades to 64 or 128 Kb to facilitate running CP/M 2.2.

The Microbee was distinct from it's competitors in having a relatively high resolution video output ( 64x16/80x24 characters or 512x256 pixels ).

This was counterbalanced by lack of colour.  And the hi-res video mode was only partially bitmapped due to a lack of screen RAM.

Plus there was a rather poor monophonic speaker output ( compared to competitors such as the C64 )
 
I spent many happy hours messing about with it before time marched on and I ( and everyone else ) moved onto PC compatibles.

But I have always had a soft spot for the 'Bee.

I came across a truly excellent PC-based emulator called [uBee512](https://www.microbee-mspp.org/repository/ "Microbee Software Preservation Project Repository").

I spent many hours trying to build the source code under MacOS.  

Whilst eventually successful, it lead me to wonder whether or not I could build my own emulator.

So I have started on this massive undertaking and documenting my progress.

Further information can be found at :

- [Wikipedia](https://en.wikipedia.org/wiki/MicroBee "Wikipedia")
- [Microbee Software Preservation Project](https://microbee-mspp.org/forum/index.php "Microbee Software Preservation Project")
- [Microbee Technology Forum](https://microbeetechnology.com.au/forum/ "Microbee Technology Forum")
- [Microbee Users Group](https://www.facebook.com/groups/100158753790849/ "Microbee Users Group")

### Related posts

<ul class="post-list">
{% for tag in site.tags %}
  {% if tag[0] == "Microbee" %}
     {% for post in tag[1] %}
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        {{ post.date | date: date_format }}<br>
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        {{ post.excerpt }}
     {% endfor %}
  {% endif %}
{% endfor %}
</ul>