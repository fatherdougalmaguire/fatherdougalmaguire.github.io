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

<ul>
  {% for post in site.posts %}
      {{ post.date | date: date_format }}
      <br>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
  {% endfor %}
</ul>
 