---
title: Template draft
date: '2000-01-01 00:00:00'
tags: [draft]
published: true
---

Plantilla para nuevos posts. Por defecto NO publicados


 ```
	title: Template draft
	date: '2000-01-01 00:00:00'
	tags: [draft]
	published: false
 ```

 ``` html
<img src="{{#if posts.[0]}}{{posts.[0].author.image}}{{else}}{{post.author.image}}{{/if}}" class="profile-image" alt="My Profile Photo"/>
```
