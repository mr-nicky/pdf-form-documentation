# Примеры вывода данных

## Дата начала действия полиса

`{{policy.valid_from|date:"Y"}}`

```
<span style="margin-right: 25px;">от «{{ policy.valid_from|date:"d" }}
  {% if policy.valid_from.month == 1 %}Января
  {% elif policy.valid_from.month == 2 %}Февраля
  {% elif policy.valid_from.month == 3 %}Марта
  {% elif policy.valid_from.month == 4 %}Апреля
  {% elif policy.valid_from.month == 5 %}Мая
  {% elif policy.valid_from.month == 6 %}Июня
  {% elif policy.valid_from.month == 7 %}Июля
  {% elif policy.valid_from.month == 8 %}Августа
  {% elif policy.valid_from.month == 9 %}Сентября
  {% elif policy.valid_from.month == 10 %}Октября
  {% elif policy.valid_from.month == 11 %}Ноября
  {% elif policy.valid_from.month == 12 %}Декабря
  {% endif %}»
</span>
<span>{{policy.valid_from|date:"Y"}} г.</span>
```

## Получение идентификатора собственника

`owner.id`

```
{% if owner.id != insurant.id %}
  {{ owner }}
{% endif %}
```

## Получение телефона и почт. ящика

```
<span class="visible-first-child_parent">
{% for cred in insurant.contact.all %}
{% if cred.contact_type.code == 'PHONE' %}
<span class="visible-first-child">+7{{ cred.data }}</span>
{% endif %}
{% endfor %}
</span>,
<span class="visible-first-child_parent">
{% for cred in insurant.contact.all %}
{% if cred.contact_type.code == 'EMAIL' %}
<span class="visible-first-child">{{ cred.data }}</span>
{% endif %}
{% endfor %}
</span>
```

[Главная страница][e74ac48e]

[e74ac48e]: readme.md "Начальная страница"
