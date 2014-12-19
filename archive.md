---
layout: default
permalink: /archive/
---

<ul>
{% for post in site.posts %}
{% if post.type != 'link' %}
	<li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_long_string }})</li>
{% endif %}
{% endfor %}
</ul>