---
layout: page
title: SuperSearch
permalink: /supersearch/
---

<link rel="stylesheet" href="https://miquelmariano.github.io/supersearch/super-search.css">

            <a href="javascript:void(0)" title="or press 'ESC' to search" onclick="toggleSearch()" class="search-btn">
              <img src="https://miquelmariano.github.io/assets/images/search-icon.png">
            </a>

 <div class="super-search" id="js-super-search">
  <input type="text" placeholder="Type here to search" class="super-search__input" id="js-super-search__input">
  <ul class="super-search__results" id="js-super-search__results"></ul>
 </div>

 <script src="https://miquelmariano.github.io/supersearch/super-search.js"></script>
 <script>superSearch({searchFile: '//miquelmariano.github.io/feed.xml'});
 </script>
            