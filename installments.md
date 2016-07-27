# Порядок оплаты страховой премии

```
<table>
  <tbody>
  {% if installments.0 %}
  <tr>
    <td>1-й взнос</td>
    <td><b>{% if installments.0.amount %}{{ installments.0.amount|floatformat:2|customintcomma }}{% endif %}</b>
    </td>
    <td> срок оплаты до:</td>
    <td><b>{{ installments.0.date|date:"d.m.Y" }}</b></td>
  </tr>
  {% endif %}

  {% if installments.1 %}
  <tr>
    <td>2-й взнос</td>
    <td><b>{% if installments.1.amount %}{{ installments.1.amount|floatformat:2|customintcomma }}{% endif %}</b>
    </td>
    <td> срок оплаты до:</td>
    <td><b>{{ installments.1.date|date:"d.m.Y" }}</b></td>
  </tr>
  {% endif %}

  {% if installments.2 %}
  <tr>
    <td>3-й взнос</td>
    <td><b>{% if installments.2.amount %}{{ installments.2.amount|floatformat:2|customintcomma }}{% endif %}</b>
    </td>
    <td> срок оплаты до:</td>
    <td><b>{{ installments.2.date|date:"d.m.Y" }}</b></td>
  </tr>
  {% endif %}

  {% if installments.3 %}
  <tr>
    <td>4-й взнос</td>
    <td><b>{% if installments.3.amount %}{{ installments.3.amount|floatformat:2|customintcomma }}{% endif %}</b>
    </td>
    <td> срок оплаты до:</td>
    <td><b>{{ installments.3.date|date:"d.m.Y" }}</b></td>
  </tr>
  {% endif %}

  </tbody>
</table>
```

[Главная страница][e74ac48e]

[e74ac48e]: readme.md "Начальная страница"
