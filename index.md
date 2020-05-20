---
layout: default
title:  "A.R.T.S."
---

{% if page.url != '/search.html' %}
<form action="/search.html" method="get">
    <label for="search_box">Search</label>
    <input type="text" id="search_box" name="query">
    <input type="submit" value="search">
</form>
<hr>
{% endif %}

| Title | Excerpt |
|:---:|:---:|
{% for post in site.posts -%}
| [{{ post.title }}]({{ post.url }}) | {{ post.excerpt | strip_html}} |
{% endfor -%}