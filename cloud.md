---
title: "Mo tags, mo often"
layout: page
---



<!-- from https://nathan.gs/2024/01/04/tags-in-jekyll-wordcloud/ -->

<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<script src="/assets/js/jqcloud.min.js"></script>

<div class="wordcloud" style="height: 400px; width: 90%"></div>

<script>
  function AllPosts() 
    {
      debugger;
      var alltags = [];
      {% assign bob = site.categories %}
      {% assign my_posts = site.posts | sort: "date"  %} 
      {% for ken in bob reversed offset: 1 %}
        {% for post in my_posts %}
          {% for my_tag in post.tags %}
              {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
              alltags.push({categories: "{{ken[0]}}", tag : "{{my_tag}}", title: "{{ post_title }}", date : "{{ post.date | date: date_format}}" });
          {% endfor %}
        {% endfor %}
      {% endfor %}
    }
</script>

<script>
  $(document).ready(function() 
    {
      var tags = [];
      var ed = "";
      {% for tag in site.tags %}
        {% assign tag_name = tag | first %}
        {% assign tag_weight = tag | last | size %}
        ed = "{{ tag_name }}";
        tags.push({text: "{{ tag_name }}", weight: {{ tag_weight }}, handlers: {click: function(ed) { tagClicked(ed) }}});
      {% endfor %}
      AllPosts();
      $(".wordcloud").jQCloud(tags, {shape: 'rectangular'});
    });
</script>

<script>
  function tagClicked(manny) 
    {
      debugger;
      var ed = manny.currentTarget.innerText;
      {% assign myed = ed %}
      var selectedtags = document.getElementById("selectedtags");
      selectedtags.innerHTML = "";
      {% assign bob = site.categories %}
      {% assign my_posts = site.posts | sort: "date"  %} 
      {% for ken in bob reversed offset: 1 %}
        selectedtags.innerHTML = selectedtags.innerHTML + '<h1>{{ken[0] | capitalize }}</h1><ul class="post-list">';
        {% for post in my_posts %}
          {% for my_tag in post.tags %}
          /*
          {{ myed }}   
          {{my_tag }}
          {{my_tag | size }} 
          */
            {% if post.categories[1] == ken[0] and my_tag == "Z80" %}
              {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
              selectedtags.innerHTML = selectedtags.innerHTML +'{{ post.date | date: date_format }}<h3><a href="{{ post.url }}">{{ post.title }}</a></h3><hr>';
            {% endif %}
          {% endfor %}
        {% endfor %}
        selectedtags.innerHTML = selectedtags.innerHTML + "</ul>";
      {% endfor %}
    }
</script>

<div id="selectedtags"></div>

{%comment%}
{% assign bob = site.categories %}
{% assign my_posts = site.posts | sort: "date"  %}
{% for ken in bob reversed offset: 1 %}
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
{%endcomment%}
