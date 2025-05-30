---
title: "Search"
layout: page
---

<p style="text-align:center;">Can't find what you are looking for ?</p>

<!-- from https://github.com/jekyll/minima/issues/741 -->

 <!-- Search Input -->
<input type="text" id="search-input" placeholder="Search...">

<!-- Results Display -->
<ul id="search-results"></ul>

<!-- Initialization Script -->
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('search-results'),
    json: '/search.json',
    searchResultTemplate: '<li><a href="{url}" title="{title}">{title}</a><br><small>{excerpt}</small></li>',
    noResultsText: 'No results found'
  });
</script>