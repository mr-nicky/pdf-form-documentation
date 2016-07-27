# Вывод документа

Пример вывода документов

```
<table>
  <tbody>
  <tr>
    <td> Паспорт №</td>
    <td class="visible-first-child_parent">
      {% for cred in insurant.credential.all %}
      {% if cred.credential_type.code == 'INTERNAL_RUSSIAN_PASSPORT' %}
        <span class="visible-first-child">
            {{ cred.series }} № {{ cred.number }}
        </span>
      {% endif %}
      {% endfor %}
    </td>
    <td>дата</td>

    <td class="visible-first-child_parent">
      {% for cred in insurant.credential.all %}
      {% if cred.credential_type.code == 'INTERNAL_RUSSIAN_PASSPORT' %}
        <span class="visible-first-child">
            {{ cred.issue_date }}
        </span>
      {% endif %}
      {% endfor %}
    </td>
    <td> выдан</td>

    <td class="visible-first-child_parent">
      {% for cred in insurant.credential.all %}
      {% if cred.credential_type.code == 'INTERNAL_RUSSIAN_PASSPORT' %}
        <span class="visible-first-child">
            {{ cred.issue_point }}
        </span>
      {% endif %}
      {% endfor %}
    </td>
  </tr>
  </tbody>
</table>
```

[Главная страница][e74ac48e]

[e74ac48e]: readme.md "Начальная страница"
