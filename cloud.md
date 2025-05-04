---
title: "Mo tags, mo often"
layout: page
---

<!-- from https://nathan.gs/2024/01/04/tags-in-jekyll-wordcloud/ -->

<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<script src="/assets/js/jqcloud-1.0.5.js"></script>

<div class="wordcloud" style="height: 400px; width: 90%"></div>

<div hidden id="tag_list"></div>
<div hidden id="taggy_list"></div>

<div id="selectedtags"></div>

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
      {%- assign bob = site.categories -%}
      {%- assign my_posts = site.posts | sort: "date"  -%} 
      {% for ken in bob reversed offset: 1 %}
        {% for post in my_posts %}
           {%- if ken[0] == post.categories.last -%}
              alltags.push({category: "{{ken[0] | capitalize }}", tag : '{{ post.tags | split: "+" }}', title: "{{ post.title }}", excerpt: {{ post.excerpt | strip | strip_html | strip_newlines | escape | jsonify }},date : "{{ post.date | date: '%Y-%m-%dT%H:%M:%SZ' }}", url : "{{ post.url}}", month_date : "{{ post.date | date: '%B %Y' }}"});
            {%- endif -%}
        {% endfor %}
      {%- endfor -%}
      return alltags;
    }

    function tagClicked(manny) 
    {
      /*debugger;*/
      console.log("------");
      /*var ed = manny.currentTarget.innerText;*/
      var selectedtags = document.getElementById("selectedtags");
      selectedtags.innerHTML = "";
      var arrayLength = listotags.length;
      var currentCategory = "";
      var currentMonth = "";
      var bobby = document.getElementById("taggy_list").innerText.slice(0,-1);
      var jonny = bobby.split("|").sort();
      for (var i = 0; i < arrayLength; i++)
      {
        console.log("------");
        console.log("parsed page tags:"+jonny);
        var billy = listotags[i].tag.replace('[','').replace(']','').replace(/"/g,'').replace(/, /g,',').split(",").sort();
        console.log("parsed post tags:"+billy);
        console.log("ccommon tags:"+jonny.filter(el => billy.includes(el)));
        var steve = jonny.filter(el => billy.includes(el)).length;
        console.log("size of common tags:"+steve);
        console.log("LOT-title"+listotags[i].title);
      /* if (listotags[i].tag.toUpperCase() == manny.toUpperCase())*/
        if (steve != 0)
       {
          if  (currentCategory != listotags[i].category )
          {
            currentCategory = listotags[i].category;
            selectedtags.innerHTML = selectedtags.innerHTML + "<h3>" + currentCategory + '</h3><ul class="post-list">';
            currentMonth = listotags[i].month_date;
            selectedtags.innerHTML = selectedtags.innerHTML + "<p style="+'"'+"text-indent: 15px;"+'"'+">"+currentMonth+"</p>";
          }
          if ( currentMonth != listotags[i].month_date )
          {
           currentMonth = listotags[i].month_date;
           selectedtags.innerHTML = selectedtags.innerHTML + "<p style="+'"'+"text-indent: 15px;"+'"'+">"+currentMonth+"</p>";
          }
           selectedtags.innerHTML = selectedtags.innerHTML + "<p style="+'"'+"text-indent: 30px;"+'"'+"><a href="+'"'+listotags[i].url+'"'+" title="+'"'+listotags[i].excerpt+'"'+">"+listotags[i].title+"</a></p>";
      }
        selectedtags.innerHTML = selectedtags.innerHTML + "</ul>";
      }
    }

      function bum(eddie)
        {
          /*debugger;*/
          var ed = eddie.currentTarget.innerText;
          var allListElements = $( "[id*='_word_']" );
          for (var i = 0; i < allListElements.length; i++)
          {
            var tagindex = tags.findIndex(x => x.text === ed );
            /*console.log(allListElements[i]);
            console.log(allListElements[i].innerText);
            console.log(allListElements[i].className);
            console.log(tags[i].text);
            console.log(tags[i].selected);*/
            if (allListElements[i].innerText == ed)
              {
             /*   console.log("@ed:"+ed);
                console.log("@ALE:"+allListElements[i].innerText);
                console.log("@tagsTxt:"+tags[tagindex].text);
                console.log("@tagsel:"+tags[tagindex].selected);*/
                if (tags[tagindex].selected == 0)
                {
                  $(allListElements[i]).css("color", "red");
                  tags[tagindex].selected = 1;
                }
                else
                {
                  $(allListElements[i]).css("color", "blue");
                  tags[tagindex].selected = 0;
                }
            /*    console.log("*ed:"+ed);
                console.log("*ALE:"+allListElements[i].innerText);
                console.log("*tagsTxt:"+tags[tagindex].text);
                console.log("*tagsel:"+tags[tagindex].selected);*/
              } 
          }
          var ken = "";
          if (first_run)
          {
            ken = document.getElementById("taggy_list").innerHTML;
            first_run = false;
          }
          for (var i = 0; i < tags.length; i++)
          {
           if (tags[i].selected == 1)
             {
              ken = ken+tags[i].text+"|"; 
             }
          }
          document.getElementById("taggy_list").innerHTML = ken; 
          document.getElementById("tag_list").innerHTML = ed;
          tagClicked(ed);
        }

      var tags = [];
      var listotags = [];
      var ed = "";
      var first_run = true;
      const searchParams = new URLSearchParams(window.location.search)
      {% for tag in site.tags %}
        {%- assign tag_name = tag | first -%}
        {%- assign tag_weight = tag | last | size -%}
        ed = "{{ tag_name }}";
        tags.push({text: "{{ tag_name }}", weight: {{ tag_weight }}, handlers: {click: function(ed) { bum(ed) }}, selected : 0});
      {% endfor %}
      listotags = AllPosts();
      multiSort(listotags, ['category:desc','date:asc']);
      $(".wordcloud").jQCloud(tags);
      if (searchParams.has('id'))
        {
          document.getElementById("tag_list").innerHTML = searchParams.get('id');
          document.getElementById("taggy_list").innerHTML = searchParams.get('id')+"|";
          bum(searchParams.get('id'));
          /* set tag selected */
      }
    });
</script>


