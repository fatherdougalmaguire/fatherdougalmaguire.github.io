---
#permalink: /corewars/
title: "CoreWars"
layout: post
---

Core War pits two programs ( written in simplified programming language called RedCode ) against each other in a virtual computer ( called M.A.R.S or Memory Array Redcode Simulator )

Each program battles each other in attempt to stop the other executing and essentially "win"

My implementation is called LifeOnMars.

It is written for MacOS Sonoma ( v14.0+ ) using Swift/SwiftUI.

LifeOnMars can be found [here](https://github.com/fatherdougalmaguire/LifeOnMARS "LifeOnMars GitHub repository")

![pMARS screenshot](/assets/images/pmarssdl.png "pMARS screenshot")

### Related posts

<ul class="post-list">
{% for tag in site.tags %}
  {% if tag[0] == "CoreWars" %}
     {% for post in tag[1] %}
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        {{ post.date | date: date_format }}<br>
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        {{ post.excerpt }}
     {% endfor %}
  {% endif %}
{% endfor %}
</ul>
 