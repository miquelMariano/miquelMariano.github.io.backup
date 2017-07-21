---
layout: page
title: SuperSearch
permalink: /supersearch/
---

<center>

<iframe height='454' width='300' frameborder='0' allowtransparency='true' scrolling='no' src='https://www.strava.com/athletes/4848838/latest-rides/c4b86fee8a0c26e45dd56ce2a9917ac7cb8c22d9'></iframe>

</center>

<link rel="stylesheet" href="super-search.css">
<body>

 <h2>Presiona ESC o '/' para abrir la busqueda</h2>
 <div class="super-search" id="js-super-search">
  <a href="javascript:void(0)" onclick="superSearch.toggle()" class="super-search__close-btn">X</a>
  <input type="text" placeholder="Type here to search" class="super-search__input" id="js-super-search__input">
  <ul class="super-search__results" id="js-super-search__results"></ul>
 </div>

 <script src="super-search.js"></script>
 <script>superSearch({
 	// Change to your own rss feed file path
 	searchFile: '//miquelmariano.github.io/feed/rss.xml'
 });</script>
</body>
</link>