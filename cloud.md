---
title: "Mo tags, mo often"
layout: page
---

{% assign bob = site.categories %}
{% assign my_posts = site.posts | sort: "date"  %}
{% assign jerry = "" %}

{% for ken in bob reversed %}
  {%if forloop.last %}
  {%else%}
  {{ jerry | append: ken[0]}}
  {%endif%}
{% endfor %}  
{{jerry}}
{% for ken in bob offset: 1 %}
  <h1>{{ken[0] | capitalize }}</h1>
  <ul class="post-list">
  {% for post in my_posts %}
    {% if post.categories[1] == ken[0] %}
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        {{ post.date | date: date_format }}
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        {{ post.excerpt }}
        <hr>
    {%endif%}
  {% endfor %}
  </ul>
{% endfor %}