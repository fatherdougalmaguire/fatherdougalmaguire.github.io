---
#permalink: /corewars/
title: "CoreWars"
layout: post
---

![pMARS screenshot](/assets/images/pmarssdl.png "pMARS screenshot")

<br>
I first read about CoreWars in old back issues of Scientific American.  
And I was hooked.

CoreWars pits two programs ( written in simplified programming language called RedCode ) against each other in a virtual computer ( called M.A.R.S or Memory Array Redcode Simulator )

Each program battles each other in attempt to stop the other executing and essentially win the battle.

Within this framework, these programs ( or warriors ) need to rely on complex strategies to defeat their opponents.  

Further,  genetic programming can be used to evolve warriors.

I'm going to document my experience on building a MacOS MARS environment in these pages.

Further information can be found at :

- [Wikipedia](https://en.wikipedia.org/wiki/Core_War "Wikipedia")
- [Core War - the Ultimate Programming Game](https://corewar.co.uk/ "Core War - the Ultimate Programming Game")

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
 