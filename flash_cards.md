{% for flash_card in site.flash_cards %}

  <h1>{{ flash_card.term }}</h1>
  <h2>{{ flash_card.definition }}</h2>
  <p>{{ flash_card.content | markdownify }}</p>

{% endfor %}
