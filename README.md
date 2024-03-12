# Проектирование архитектуры информационных систем
По состоянию на март 2024 у меня мало знаний в части [архитектуры ПО](https://agaltsovav.ru/docs/architecture/), но это то направлени в котором я хочу развиваться.
Начинаю экспиремент по совмещению техник и инструментов Предметно-Ориентированного Проектирование и Объектно-Ориентированного Программирования.<br>
Мотивцией послужило выгорание при работе над текущим проектом и желание погрузиться в изучение UML и python.<br>
В процессе экспиремента так же считаю необходимым изучение [паттернов проектирования](https://github.com/pkolt/design_patterns?tab=readme-ov-file).




## План экспиримента (последовательность шагов не является строгой):
1. На практике погрузиться в ОО Программирование и прочитать книгу «Паттерны объектно-ориентированного проектирования»
2. Использовать связки **С4 и plantUML** [1](https://github.com/plantuml-stdlib/C4-PlantUML), [2](https://github.com/team7katas/sysopsquad) и оставлять шаблоны в специальном репозитории для дальнейшего переиспользования
3. Погрузиться в ПО Проектиование, прочитав книгу [«Что такое предметно-ориентированное проектирование?"](https://systems.education/what-is-domain-driven-design) и практиковать Event Storming, по-возможности
4. Написать ТЗ для пет-проекта используя обе практики
5. Релализовать пет-проект (в том числе с привлеченим аутсорса), используя микросервисную архитектуру



## Глава 1. Погружение в ООП
**Объект - коллекция/набор данных и поведения ИЛИ данные с ассоциируемым поведением.**
<br>
*Объектно-ориентированный Python (4 издание) // Стивен Ф. Лотт, Дастин Филлипс*


Я знаком с базовыми концепциями ООП, но всегда избегал его при написании кода, чтобы исправиться начну рефакторинг кода для игры ["Висилеца"](https://github.com/sqrt495/OOP-python-learning/blob/main/Hangman.ipynb) написанного мной после знакомства с курсом самообучения от [Сергея Жукова](https://zhukovsd.github.io/python-backend-learning-course/).


### Знакомство с паттернами ООП 
**Мы будем классифицировать паттерны по двум критериям. Первый — цель — отражает назначение паттерна. Паттерны делятся на порождающие, структурные и паттерны поведения. Первые связаны с процессом создания объектов. Вторые имеют отношение к композиции объектови классов. Паттерны поведения характеризуют то, как классы или объекты взаимодействуют.
Второй критерий — уровень — сообщает, к чему обычно применяется паттерн: к объектам или классам. Паттерны уровня классов описывают отношения между классами и их подклассами. Такие отношения выражаются с помощью наследования, поэтому они статичны, то есть зафиксированы на этапе компи￾ляции. Паттерны уровня объектов описывают отношения между объектами, которые могут изменяться во время выполнения и потому более динамичны. Почти все паттерны в какой-то мере используют наследование. Поэтому к категории «паттерны классов» отнесены только те, что концентрируются лишь на отношениях между классами. Обратитевнимание: большинство паттернов действует на уровне объектов.
Существуют и другие способы классификации паттернов. Некоторые паттерны часто используются вместе. Например, 'компоновщик' применяется с 'итератором' или'посетителем'. Некоторыми паттернами предлагаются альтернативные решения. Так, 'прототип' нередко можно использовать вместо 'абстрактной фабрики'. Применение части паттернов приводит к схожему дизайну, хотя изначально их назначение различно. Например, структурные диаграммы 'компоновщика' и 'декоратора' похожи.**

<img src="OOP_patterns_form_book.png" alt="patterns" width="800"/>

*Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 28* 
