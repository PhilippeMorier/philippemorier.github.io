| Title | Definition |
| ----- | ---------- |
{% for flash_card in site.flash_cards -%}
| [{{ flash_card.title }}]({{ flash_card.url}}) | {{ flash_card.definition }} |
{% endfor -%}
