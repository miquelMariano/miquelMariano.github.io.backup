---
layout: page
title: SuperSearch
permalink: /supersearch/
---

            
 <link rel="stylesheet" href="/supersearch/super-search.css">

  <a href="javascript:void(0)" title="or press '/' to search" onclick="toggleSearch()" class="search-btn">
    <img src="/images/search-icon.png">
         </a>

            <div class="super-search" id="js-super-search">
               <a href="javascript:void(0)" onclick="superSearch.toggle()" class="super-search__close-btn">X</a>
               <input type="text" placeholder="Type here to search" class="super-search__input" id="js-super-search__input">
               <ul class="super-search__results" id="js-super-search__results"></ul>
            </div>

             <script src="/supersearch/super-search.js"></script>
             <script>superSearch({
                // Change to your own rss feed file path
                                   searchFile: '//miquelmariano.github.io/feed.xml'
                                  });
             </script>
            