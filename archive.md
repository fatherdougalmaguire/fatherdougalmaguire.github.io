---
title: Archive
layout : page
---

<!--  old CDN list
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js" integrity="sha512-v2CJ7UaYy4JwqLDIrZUI/4hqeoQieOmAZNXBeQyjo21dadnwR+8ZaIJVT8EE2iyI61OV8e6M8PP2/4hpQINQ/g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script> 
-->

<script src="/assets/js/jquery-3.7.1.min.js"></script>

<!-- from https://github.com/mistic100/jQCloud -->
<script src="/assets/js/jqcloud.min.js"></script>

<p align=center><b>Click on one or more tags to display matching posts.</b></p>

<div class="wordcloud" style="height: 400px; width: 90%"></div>

<div hidden id="tag_list"></div>

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

  function BuildAllPostList() 
    {
      /*debugger;*/
      var alltags = [];
      {%- assign all_categories = site.categories -%}
      {%- assign my_posts = site.posts | sort: "date"  -%} 
      {% for my_category in all_categories reversed offset: 1 %}
        {% for post in my_posts %}
           {%- if my_category[0] == post.categories.last -%}
              alltags.push({category: "{{my_category[0] | capitalize }}", tag : '{{ post.tags | split: "+" }}', title: "{{ post.title }}", excerpt: {{ post.excerpt | strip | strip_html | strip_newlines | escape | jsonify }},date : "{{ post.date | date: '%Y-%m-%dT%H:%M:%SZ' }}", url : "{{ post.url}}", month_date : "{{ post.date | date: '%B %Y' }}"});
            {%- endif -%}
        {% endfor %}
      {%- endfor -%}
      return alltags;
    }

  function BuildPostList() 
    {
      var selectedtags = document.getElementById("selectedtags");
      selectedtags.innerHTML = "";
      var arrayLength = listotags.length;
      var currentCategory = "";
      var currentMonth = "";
      var retrieve_selected_tags= document.getElementById("tag_list").innerText.slice(0,-1);
      var selected_tags_array = retrieve_selected_tags.split("|").sort();
      for (var i = 0; i < arrayLength; i++)
      {
        var sorted_tags= listotags[i].tag.replace('[','').replace(']','').replace(/"/g,'').replace(/, /g,',').split(",").sort();
        var sorted_tags_length= selected_tags_array.filter(el => sorted_tags.includes(el)).length;
        if (sorted_tags_length != 0)
       {
          if (currentCategory != listotags[i].category )
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
           selectedtags.innerHTML = selectedtags.innerHTML + "<p class="+'"'+"archive_title"+'"'+"><a href="+'"'+listotags[i].url+'"'+" title="+'"'+listotags[i].excerpt+'"'+">"+listotags[i].title+"</a></p>";
      }
        selectedtags.innerHTML = selectedtags.innerHTML + "</ul>";
      }
    }

      function BuildTagList(passed_tag,first_run)
        {
  
          if (first_run)
            {
              var tag_match = passed_tag;
            }
            else
            {
              var tag_match = passed_tag.currentTarget.innerText;
            }
          var allListElements = $( "[id*='_word_']" );
          for (var i = 0; i < allListElements.length; i++)
          {
            var tagindex = tags.findIndex(x => x.text === tag_match );
            if (allListElements[i].innerText == tag_match)
              {
                if (tags[tagindex].selected == 0 || first_run )
                {
                  $(allListElements[i]).removeClass(tags[tagindex].tag_class);
                  $(allListElements[i]).addClass(tags[tagindex].tag_class+"plus");
                  tags[tagindex].selected = 1;
                }
                else
                {
                  $(allListElements[i]).removeClass(tags[tagindex].tag_class+"plus");
                  $(allListElements[i]).addClass(tags[tagindex].tag_class);
                  tags[tagindex].selected = 0;
                }
              } 
          }
          var selected_tags = "";
          if (first_run)
          {
            selected_tags = document.getElementById("tag_list").innerHTML;
          }
          for (var i = 0; i < tags.length; i++)
          {
           if (tags[i].selected == 1)
             {
              selected_tags = selected_tags+tags[i].text+"|"; 
             }
          }
          document.getElementById("tag_list").innerHTML = selected_tags; 
          BuildPostList();
        }
  
      function firsttag()
      {
        const searchParams = new URLSearchParams(window.location.search);
        var allspan = $( "[id*='_word_']" );
          for (var i = 0; i < allspan.length; i++)
          {
            for (var j = 0; j < tags.length; j++)
            if (allspan[i].innerText == tags[j].text)
              {
                tags[j].tag_class = allspan[i].className;
              } 
          }
        if (searchParams.has('id'))
        {
          document.getElementById("tag_list").innerHTML = searchParams.get('id')+"|";
          BuildTagList(searchParams.get('id'),true);
          /* set tag selected */
        }
      }

      var tags = [];
      var listotags = [];
      var current_tag_name = "";
      
      {% for tag in site.tags %}
        {%- assign tag_name = tag | first -%}
        {%- assign tag_weight = tag | last | size -%}
        current_tag_name = "{{ tag_name }}";
        tags.push({text: "{{ tag_name }}", weight: {{ tag_weight }}, handlers: {click: function(current_tag_name) { BuildTagList(current_tag_name,false)}}, selected : 0, tag_class : ""});
      {% endfor %}
      multiSort(listotags, ['category:desc','date:asc']);
      $(".wordcloud").jQCloud(tags, {removeOverflowing: true, afterCloudRender: function() { firsttag() }} );
      listotags = BuildAllPostList();
    });
</script>


