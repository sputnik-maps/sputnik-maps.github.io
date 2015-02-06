---
layout: page
title: Sputnik.Maps GitHub
permalink: /
---

# Projects
{% for node in site.pages %}
{% if node.group == "projects" %}
* [{{node.title}}]({{node.url}})
{% endif %}
{% endfor %}

