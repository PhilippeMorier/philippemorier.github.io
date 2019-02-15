---
layout: default
---

# {{ page.term }}

{{ page.definition }}

{{ page.content }}

{% for tag in page.tags %}
`{{ tag }}`
{% endfor %}
