# Генерация адреса

Пример вывода адреса

```
/* Проверка на пустое значение (дом, корпус) в адресе */
.b-pdf__address:empty:before {
  content: '' !important;
}

.b-pdf__address:empty:after {
  content: '' !important;
}

.b-pdf__address--korpus:before {
  content: ', кор. ';
}

.b-pdf__address--stroenie:before {
  content: ', стр. ';
}

.b-pdf__address--kvartira:before {
  content: ', кв. ';
}

.b-pdf__address--pomeshenie:before {
  content: ', пом. ';
}
```

```
<span class="visible-last-child_parent">
  {% for address in insurant.address.all %} {% if address.address_type.code == 'ACTUAL_ADDRESS' %}
  <span class="visible-last-child">
   {% if address.postal_index %}{{ address.postal_index }},{% endif %}
   {{ address.country }}, {{ address.city }}, {{ address.street }}, дом {{ address.house }}
    <span class="b-pdf__address b-pdf__address--korpus">{{ address.housing | default:'' }}</span>
    <span class="b-pdf__address b-pdf__address--stroenie">{{ address.structure | default:'' }}</span>
    <span class="b-pdf__address b-pdf__address--kvartira">{{ address.flat | default:'' }}</span>
    <span class="b-pdf__address b-pdf__address--pomeshenie">{{ address.apartment | default:'' }}</span>
  </span>
  {% endif %}
  {% endfor %}
</span>
```

[Главная страница][e74ac48e]

[e74ac48e]: readme.md "Начальная страница"
