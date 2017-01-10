---
title: Template draft
date: '2000-01-01 00:00:00'
tags: [draft]
published: true
---


``` html
<img src="{{#if posts.[0]}}{{posts.[0].author.image}}{{else}}{{post.author.image}}{{/if}}" class="profile-image" alt="My Profile Photo"/>
```

Add this to your css file:

``` css
.profile-image {
      position: relative;
      width: 100px;
      height: 100px;
      border: 3px solid #fff;
      border-radius:100%;
}
```

``` 
title: Template draft
date: '2000-01-01 00:00:00'
tags: [draft]
published: true
```