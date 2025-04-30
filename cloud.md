---
title: "Mo tags, mo often"
layout: page
---



<!-- from https://nathan.gs/2024/01/04/tags-in-jekyll-wordcloud/ -->

<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<script src="/assets/js/jqcloud.min.js"></script>

<div class="wordcloud" style="height: 400px; width: 90%"></div>

<div id="tag_list"></div>

<script>
  
  $(document).ready(

    function() 
    {

      function multiSort(arr, fields) 
      {
       arr.sort((a, b) => 
      {
        for (let field of fields) 
        {
        const [fieldName, order] = field.split(':');
        const aValue = a[fieldName];
        const bValue = b[fieldName];

        if (aValue < bValue) return order === 'desc' ? 1 : -1;
        if (aValue > bValue) return order === 'desc' ? -1 : 1;
       }
      return 0;
       });
    }

  function AllPosts() 
    {
      /*debugger;*/
      var alltags = [];
      {% assign bob = site.categories %}
      {% assign my_posts = site.posts | sort: "date"  %} 
      {% for ken in bob reversed offset: 1 %}
        {% for post in my_posts %}
          {% for my_tag in post.tags %}
              {% if ken[0] == post.categories.last %}
                  alltags.push({category: "{{ken[0] | capitalize }}", tag : "{{my_tag | capitalize }}", title: "{{ post.title }}", excerpt: {{ post.excerpt | strip | strip_html | strip_newlines | escape | jsonify }},date : "{{ post.date | date: '%Y-%m-%dT%H:%M:%SZ' }}", url : "{{ post.url}}", month_date : "{{ post.date | date: '%B %Y' }}"});
              {% endif %}
          {% endfor %}
        {% endfor %}
      {% endfor %}
      return alltags;
    }

      function bum(eddie)
        {
         var ed = eddie.currentTarget.innerText;
        document.getElementById("tag_list").innerHTML = ed;
        }

      function tagClicked(manny) 
    {
      debugger;
      var ed = manny.currentTarget.innerText;
      var selectedtags = document.getElementById("selectedtags");
      selectedtags.innerHTML = "";
      var arrayLength = listotags.length;
      var currentCategory = "";
      var currentMonth = "";
      for (var i = 0; i < arrayLength; i++)
      {
       if (listotags[i].tag == ed)
       {
          if  (currentCategory != listotags[i].category )
          {
            currentCategory = listotags[i].category;
            selectedtags.innerHTML = selectedtags.innerHTML + "<h1>" + currentCategory + '</h1><ul class="post-list">';
             if ( currentMonth != listotags[i].month_date )
          {
           currentMonth = listotags[i].month_date;
           selectedtags.innerHTML = selectedtags.innerHTML + currentMonth+"<br>";
          }
          }
         
          selectedtags.innerHTML = selectedtags.innerHTML + "<h3><a href="+'"'+listotags[i].url+'">'+listotags[i].title+"</a></h3>"+listotags[i].excerpt;
      }
        selectedtags.innerHTML = selectedtags.innerHTML + "</ul>";
      }
    }

      var tags = [];
      var listotags = [];
      var ed = "";
      {% for tag in site.tags %}
        {% assign tag_name = tag | first %}
        {% assign tag_weight = tag | last | size %}
        ed = "{{ tag_name }}";
        tags.push({text: "{{ tag_name | capitalize }}", weight: {{ tag_weight }}, handlers: {click: function(ed) { tagClicked(ed) }}});
      {% endfor %}
      listotags = AllPosts();
      multiSort(listotags, ['category:desc', 'tag:asc','date:asc']);
      $(".wordcloud").jQCloud(tags, {shape: 'rectangular'});
    });
</script>

<script>
  
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
