| Term | Definition |
| ---- | ---------- |


{% for flash_card in site.flash_cards %}

{{ flash_card.term }} | {{ flash_card.definition }}

{% endfor %}
