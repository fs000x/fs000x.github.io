---
layout: default
title: My Blog
---

# {{page.title}}

## 最新文章

{% for post in site.posts %}
* {{post.data | data_to_string}} [{{post.title}}]({{post.url}})
{% endfor %}
