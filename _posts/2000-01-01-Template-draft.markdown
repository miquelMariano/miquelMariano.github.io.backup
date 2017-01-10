---
title: Template draft
date: '2000-01-01 00:00:00'
tags: [draft]
published: true
---

Insertar código HTML:

``` html
<img src="{{#if posts.[0]}}{{posts.[0].author.image}}{{else}}{{post.author.image}}{{/if}}" class="profile-image" alt="My Profile Photo"/>
```

Insertar código CSS:

``` css
.profile-image {
      position: relative;
      width: 100px;
      height: 100px;
      border: 3px solid #fff;
      border-radius:100%;
}
```

Insertar código YAML:

``` yaml
---
#Las variables deben ir siempre entre {{ dobles

- hosts: "{ servers }:!localhost"
  user: root
  serial: 15
  roles:
   - "miquelMariano.ESXi_{ role }"

```

Insertar código sin especificar lenguaje:

``` 
title: Template draft
date: '2000-01-01 00:00:00'
tags: [draft]
published: true
```