# Документация по верстке печатных форм

## Генерация форм

- На backend'е работает на Python'е (версия 2.7).
- При верстке печатных форм используем встроенный шаблон тегов и фильтров Djungo (Версия 1.6). Документация [здесь][a52bd164].
- Формы генерируются с помощью Weasyprint (Версия 0.23). Документация [здесь][6b56bcea].

В верху печатной формы, после `<!DOCTYPE html>` написать строку: `{% load main_tags %}`

1. [Генерация адреса][dbf2ef73]
2. [Вывод водителей][a950bc67]
3. [Примеры вывода данных][135f8748]
4. [Стили помощники][4bf88a59]
5. [Вывод документа][d0e15a37]
6. [Порядок оплаты страховой премии][4b35ec9a]

## Объекты справочников

**Справочник** – все, что настраивается/добавляется через админку. Возвращает строку по умолчанию.

Объект с полями `id`, `title`, `code` и пр. См. в админку.

Название                            | Ссылка на админку
:---------------------------------- | :--------------------------
Тип ТС                              | /admin/main/cartype/
Страховая сумма                     | /admin/main/insurancesum/
Срок действия договора              | /admin/main/riskgroup/
Тип франшизы                        | /admin/main/deductibletype/
Типы выплат страховой суммы         | /admin/main/paymenttype/
Формы выплаты страхового возмещения | /admin/main/paymentform/
Цели использования                  | /admin/main/targetofusing/
Цель поездки                        | /admin/main/trippurpose/
И т.д. Смотреть:                    | /admin/main/

## Типы документов

В каждом типе объекта используется свой набор типов документов. Например, у водителя используется `DRIVER_LICENSE`, у ТС – `VEHICICLE_REGISTRATION` и т.д. Все типы документов смотреть здесь: `/admin/client/credentialtype/`

```
<div class="visible-last-child_parent">
  {% for cred in driver.credential.all %}
  {% if cred.credential_type.code == 'DRIVER_LICENSE' %}
    <span class="visible-last-child">{{cred.series}} {{cred.number}} {{cred.issue_date}}</span>
  {% endif %}
  {% endfor %}
</div>
```

## Фильты

Название         | Что делает                                                  | Пример использования
:--------------- | :---------------------------------------------------------- | --------------------
`floatformat`    | Округляет число до заданного количетва знаков после запятой | `floatformat:2`
`default`        | Назначает значение по умолчанию                             | `default:''`
`date`           | Приводит дату к установленному формату                      | `date:"d.m.Y"`
`customintcomma` | Выводит запятую как разделитель в числе                     | `customintcomma`

### Пример исползования фильтров:

```
{{ storage.data.Ssum|floatformat:2|customintcomma }}
```

## Переменные

Название переменной                           | Что выводит                                    | Формат         | Пример вывода
:-------------------------------------------- | :--------------------------------------------- | :------------- | :-------------------------
`policy.pnumber`                              | Номер полиса                                   | Строка         | 0000332323
`policy.pseries`                              | Серия полиса                                   | Объект даты    | МС1
`policy.valid_from`                           | Дата начала действия полиса                    | Объект даты    | 27.07.2016
`owner`                                       | Собственник                                    | Строка         | Иванов Иван Иванович
`owner.first_name_eng`                        | Имя собственника на латинице                   | Строка         | Ivan
`owner.last_name_eng`                         | Фамилия собственника на латинице               | Строка         | Ivanov
`owner.patronymic_eng`                        | Отчество собственника на латинице              | Строка         | Ivanovich
`owner.citizenship`                           | Граждаство собственника                        | Строка         | Российская Федерация
`beneficiary`                                 | Выгодоприобретатель                            | Строка         | Иванов Иван Иванович
`drivers`                                     | Все водители                                   | Массив         | Массив всех водителей
`driver`                                      | Лицо, допущенное к управлению ТС               | Строка         | Иванов Иван Иванович
`driver.birth_date`                           | Дата рождения водетеля                         | Объект даты    | 07.07.1951
`driver.credential`                           | См. Типы документов                            | Массив         | Массив данных документа
`driver.driving_experience_started`           | Водительский стаж (дата начала вождения)       | Дата           | 07.07.1988
`cred.credential_type`                        | Тип документа (/admin/client/credentialtype/)  | ID справочника | Паспорт
`cred.series`                                 | Серия документа                                | Число          | 3345
`cred.number`                                 | Номер документа                                | Число          | 3427723
`car.car_mark`                                | Марка машины                                   | Строка         | BMW
`car.car_model`                               | Модель машины                                  | Строка         | 1er
`car.vin_number`                              | VIN номер машины                               | Строка         | XTA210990Y2766389
`car.number_plate`                            | Гос. номер автомобиля                          | Строка         | Е102СН
`car.color`                                   | Цвет машины                                    | Строка         | Белый
`car.car_mark.title`                          | Марка машины                                   | Строка         | BMW
`car.manufacturing_date.year`                 | Дата производства автомобиля                   | Число          | 2007
`document_type`                               | Тип документа                                  | ID справочника | Водительское удостоверение
`policy.creator.company.bunch`                | Набор печатных форм компании                   | ID справочника | Брутто/Брутто
`insurant`                                    | ФИО страхователя                               | Строка         | Иванов Иван Иванович
`insurant.first_name`                         | Имя страхователя                               | Строка         | Иван
`insurant.last_name`                          | Фамилия страхователя                           | Строка         | Иванов
`insurant.patronymic`                         | Отчество страхователя                          | Строка         | Иванович
`insurant.title_eng`                          | Фамилия имя отчество на английском             | Строка         | Ivanov Ivan Ivanovich
`insurant.first_name_eng`                     | Имя страхователя на латинице                   | Строка         | Ivan
`insurant.last_name_eng`                      | Фамилия страхователя на латинице               | Строка         | Ivanov
`insurant.patronymic_eng`                     | Отчество стахователя на латинице               | Строка         | Ivanovich
`insurant.inn`                                | ИНН страхователя                               | Число          | 7826678515
`insurant.ogrn`                               | ОГРН стархователя                              | Число          | 1037851019524
`insurant.gender`                             | Пол страхователя                               | F, M           | F
`insurant.birth_date`                         | Дата рождения страхователя                     | Объект даты    | 07.07.1951
`insurant.citizenship`                        | Гражданство страхователя                       | Строка         | Грузия
`insurant.representative_first_name`          | Имя представителя юр. лица                     | Строка         | Иван
`insurant.representative_last_name`           | Фамилия представителя юр. лица                 | Строка         | Иванов
`insurant.representative_patronymic`          | Отчество представителя юр. лица                | Строка         | Иванович
`insurant.representative_post`                | Должность представителя юр. лица               | Строка         | Директор
`insurant.is_individual_entrepreneur`         | Индивидуальный предпрениматель                 | Boolean        | true
`storage.data.S`                              | Страховая премия                               | Число          | 31000
`storage.data.Sdgo`                           | Гр. отв. страховая премия                      | Число          | 10000
`storage.data.Ssum`                           | Общая страховая премия                         | Число          | 15000
`storage.data.Sdo`                            | Страховая сумма ДО                             | Число          | 100000
`storage.data.Sns`                            | Страховая премия «Несчастный случай»           | Число          | 10000
`storage.data.Sdgo`                           | Страховая премия «Гражданская ответственность» | Число          | 34000
`policy.insured_object.insurant.legal_person` | Юр. лицо                                       | Строка         | ОАО "Фирма"
`insurant.representative_number`              | Номер доверенности                             | Число          | 344242
`insurant.representative_issue_date`          | Дата дейсвия доверенности                      | Объект даты    | 07.07.1951
`parameters.insurant_phone`                   | Телефон стархователя                           | Строка         | 9112993453
`parameters.insurant_email`                   | Почтовый ящик страхователя                     | Строка         | ivan@mail.ru

### calculation

Все объекты calculation – ввод данных для отправления в страховую компанию и получения расчета.

Название переменной                           | Что выводит                                                   | Формат         | Пример вывода
:-------------------------------------------- | :------------------------------------------------------------ | :------------- | :--------------------------------------
`calculation.valid_to`                        | Конец действия договора                                       | Объект даты    | 27.07.2020
`calculation.city`                            | Территория действия договора                                  | Строка         | г. Санкт-Петербург
`calculation.gender`                          | Пол                                                           | Строка         | F
`calculation.insurable_risk`                  | Страховой риск (Каско, Ущерб)                                 | ID справочника | Каско
`calculation.car_cost`                        | Старховая сумма (Стоимость машины)                            | Число          | 600000
`calculation.birth_date`                      | Дата рождения                                                 | Объект даты    | 27.07.2000
`calculation.valid_from`                      | Начало действия договора                                      | Объект даты    | 27.07.2016
`calculation.antitheft`                       | Противоугонная система                                        | Строка         | Technoblock
`calculation.optional_equipment_name`         | Наименование дополнительного оборудования                     | Строка         | Название ДО
`calculation.contributory_scheme`             | Порядок оплаты страховой премии (единовременно, рассрочку)    | ID справочника | Единовременно
`calculation.deductible_harm`                 | Безусловная франшиза, «Ущерб», «Ущерб по ДО                   | Число          | 15000
`calculation.deductible_theft`                | Безусловная франшиза, «Угон, Хищение», «Ущерб по ДО           | Число          | 15000
`calculation.deductible_value`                | Размер франшизы                                               | Число          | 15000
`calculation.is_multidrive`                   | Неограниченное количество водителей                           | Boolean        | true
`calculation.target_of_using`                 | Цель использования ТС                                         | ID справочника | Личная
`calculation.payment_type`                    | Страховая сумма по рискам: «Угон», «Ущерб»                    | ID справочника | Агрегатная
`calculation.payment_form`                    | Порядок определения размера ущерба                            | ID справочника | Ремонт ТС на СТО по выбору Страхователя
`calculation.exploitation_area`               | Территория страхования                                        | ID справочника | Северо-Западный ФО
`calculation.claim_form`                      | Порядок выплаты страхового возмещения                         | ID справочника | Без учета износа
`calculation.compensation_without_references` | Ущерб, при котором для получения выплаты не требуется справок | ID справочника | Повреждение стекол кузова - 1 раз
`calculation.optional_equipment_cost`         | Ущерб дополнительному оборудованию                            | Число          | 40000
`calculation.accident_percent`                | Страховая сумма «Несчастный случай»                           | Число          | 50000
`calculation.civil_liability_voluntary_cost`  | Страховая сумма «Гражданская ответственность»                 | Число          | 10000

#### Пример перебора документов

```
<div class="visible-first-child_parent">
    {% for cred in driver.credential.all %}
    {% if cred.credential_type.code == 'DRIVER_LICENSE' %}
    <span class="visible-first-child">{{cred.series}} {{cred.number}}</span>
    {% endif %}
    {% endfor %}
</div>
```

Некоторые переменные проверить на пустое значение можно только так:

```
{% if storage.data.Sns %}
  {{ storage.data.Sns|floatformat:2|customintcomma|default:'' }}
{% endif %}
```

[135f8748]: examples.md "Примеры вывода данных"
[4b35ec9a]: installments.md "Порядок оплаты страховой премии"
[4bf88a59]: styles.md "Стиил помощники"
[6b56bcea]: http://weasyprint.org/ "Weasyprint"
[a52bd164]: https://docs.djangoproject.com/en/1.9/ref/templates/builtins/ "Built-in template tags and filters"
[a950bc67]: drivers.md "Вывод водителей"
[d0e15a37]: document.md "Вывод документа"
[dbf2ef73]: adress.md "Вставка адреса"
