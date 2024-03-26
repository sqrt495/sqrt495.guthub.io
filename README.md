# Проектирование архитектуры информационных систем
По состоянию на март 2024 у меня мало знаний в части [архитектуры ПО](https://agaltsovav.ru/docs/architecture/), но это то направлени в котором я хочу развиваться.
Начинаю экспиремент по совмещению техник и инструментов Предметно-Ориентированного Проектирование и Объектно-Ориентированного Программирования.<br>
Мотивцией послужило выгорание при работе над текущим проектом и желание погрузиться в изучение UML и python.<br>
В процессе экспиремента так же считаю необходимым изучение [паттернов проектирования](https://github.com/pkolt/design_patterns?tab=readme-ov-file).

## Уверен, что домен можно объеденить в абстрактный класс нижнего/глубинного уровня, который в последствие детализируется. Я пока не нашел/дочитал до подтверждения.


## План экспиримента (последовательность шагов не является строгой):
1. На практике погрузиться в ОО Программирование и прочитать книгу «Паттерны объектно-ориентированного проектирования»
2. Использовать связки **С4 и plantUML** [1](https://github.com/plantuml-stdlib/C4-PlantUML), [2](https://github.com/team7katas/sysopsquad) и оставлять шаблоны в специальном репозитории для дальнейшего переиспользования
3. Погрузиться в ПО Проектиование, прочитав книгу [«Что такое предметно-ориентированное проектирование?"](https://systems.education/what-is-domain-driven-design) и практиковать Event Storming, по-возможности
4. Написать ТЗ для пет-проекта используя обе практики
5. Релализовать пет-проект (в том числе с привлеченим аутсорса), используя микросервисную архитектуру

***

## Глава 1. Погружение в ООП
> *Объект - коллекция/набор данных и поведения ИЛИ данные с ассоциируемым поведением.*
> <div align = 'right'> Объектно-ориентированный Python (4 издание) // Стивен Ф. Лотт, Дастин Филлипс // стр. 24 </div>


> *Ключевая задача моделирования объекта в объектно-ориентированном про­ ектировании - определить, какой будет внешний интерфейс данного объекта. Интерфейс - коллекция, набор атрибутов и методов, доступных для взаимо­ действия с другими объектами.*
> <div align = 'right'> Объектно-ориентированный Python (4 издание) // Стивен Ф. Лотт, Дастин Филлипс // стр. 33 </div>


Я знаком с базовыми концепциями ООП, но всегда избегал его при написании кода, чтобы исправиться начну рефакторинг кода для игры ["Висилеца"](https://github.com/sqrt495/OOP-python-learning/blob/main/Hangman.ipynb) написанного мной после знакомства с курсом самообучения от [Сергея Жукова](https://zhukovsd.github.io/python-backend-learning-course/).


### 1.1 Знакомство с паттернами ООП 

> *Мы будем классифицировать паттерны по двум критериям. Первый — цель — отражает назначение паттерна. Паттерны делятся на порождающие, структурные и паттерны поведения. Первые связаны с процессом создания объектов. Вторые имеют отношение к композиции объектови классов. Паттерны поведения характеризуют то, как классы или объекты взаимодействуют.
Второй критерий — уровень — сообщает, к чему обычно применяется паттерн: к объектам или классам. Паттерны уровня классов описывают отношения между классами и их подклассами. Такие отношения выражаются с помощью наследования, поэтому они статичны, то есть зафиксированы на этапе компи￾ляции. Паттерны уровня объектов описывают отношения между объектами, которые могут изменяться во время выполнения и потому более динамичны. Почти все паттерны в какой-то мере используют наследование. Поэтому к категории «паттерны классов» отнесены только те, что концентрируются лишь на отношениях между классами. Обратитевнимание: большинство паттернов действует на уровне объектов.
Существуют и другие способы классификации паттернов. Некоторые паттерны часто используются вместе. Например, 'компоновщик' применяется с 'итератором' или 'посетителем'. Некоторыми паттернами предлагаются альтернативные решения. Так, 'прототип' нередко можно использовать вместо 'абстрактной фабрики'. Применение части паттернов приводит к схожему дизайну, хотя изначально их назначение различно. Например, структурные диаграммы 'компоновщика' и 'декоратора' похожи.*
> <div align = 'right'> Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 28 </div>

<br><br>
<img src="OOP_patterns_form_book.png" alt="all_patterns" width="800"/>
<br>
<img src="OOP_patterns_relationship.png" alt="patterns_relationship" width="800"/>
<br><br>

> *Объект сочетает данные и процедуры для их обработки. Такие процедуры обычно называют методами или операциями. Объект выполняет операцию, когда получает запрос (или сообщение) от клиента.
Отправка запроса — это единственный способ заставить объект выполнить операцию. А выполнение операции — единственный способ изменить внутреннее состояние объекта. Из-за этих двух ограничений говорят, что внутреннее состояние объекта инкапсулировано: к нему нельзя обратиться напрямую, а его представление невидимо за пределами объекта.*
> <div align = 'right'> Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 29 </div>

> *Для любой операции, объявляемой объектом, должны быть заданы: имя операции, объекты, передаваемые в качестве параметров, и значение, возвращаемое операцией. Эту триаду называют сигнатурой операции.*
> <div align = 'right'> Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 32 </div>


> *Для любой операции, объявляемой объектом, должны быть заданы: имя операции, объекты, передаваемые в качестве параметров, и значение, возвращаемое операцией. Эту триаду называют сигнатурой операции.*<br>
> <div align = 'right'> Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 32 </div>

> **Предпочитайте композицию наследованию класса!**
> <div align = 'right'> Паттерны объектно-ориентированного проектирования (издание 2020) // Э. Гамма, Р. Хелм, Р. Джонсон, Дж. Влиссидес // стр. 40 </div>


### 1.2 UML Диаграмма классов

Условия задания: 
<br>
В городе ввели Департамент развития талантов школьников. Каждая школа по окончанию учебного года присылает данные: количество школьников, которые выступали на олимпиадах и количество школьников, которые заняли призовые места на олимпиадах. После получении данных от школ в процесс вмешивается Служба аудита, которая по своим источникам может поставить под сомнение данные, которые прислала конкретная школа. Например, по их сведениям в олимпиадах не побеждали дети от школы, а по переданным данным - побеждали. Внутренняя кухня Службы аудита нас не интересует, важно что они могут отметить данные от школы как сомнительные.  Эту обратную связь мы передаем школе, и она может повторно направить скорректированные данные в Департамент.
Необходимо разрабатать Дашборд с двумя таблицами.
<br>
1. Топ школ по количеству олимпиадников и победителей олимпиад по школам (данные, которые не вызывают сомнения у Службы аудита).
2. Топ школ, присылающих сомнительные данные по количеству корректировок
 
Задача:
<br>
Необходимо разработать диаграмму классов, которая позволит обеспечить формирование Дашборда.

Решение:
<br>
<img src="uml_class_Dashboard" alt="uml_class_Dashboard" width="800"/>
<br>


***

## Глава 2. Погружение в DDD
*Проблемно-ориентированное проектирование (DDD) — это набор принципов и схем, помогающих разработчикам создавать изящные системы объектов. При правильном применении оно приводит к созданию программных абстракций, которые называются моделями предметных областей. В эти модели входит сложная бизнес-логика, устраняющая промежуток между реальными условиями бизнеса и кодом.*
<br>
*Сущность — это «штука» в вашей системе. О них часто удобно думать существительными: люди, места и, ну, штуки.*
<br>
*У сущностей есть и индивидуальность, и жизненный цикл.*
<br>
*Думайте о сущностях скорее как о единицах поведения, нежели как о единицах данных. Попробуйте поместить логику в сущности, которые ей принадлежат. Чаще всего какие-то операции, которые вы пытаетесь добавить в модель, должна получить какая-то сущность, или при этом начинает создаваться или извлекаться новая сущность. В более слабом коде можно найти массу служебных или управляющих классов, проверяющих сущности снаружи. В целом я предпочитаю делать это изнутри сущности — вы получаете все преимущества, связанные с фундаментальным принципом инкапсуляции, а сущности приобретают поведение.*
<br>
**[Learn / MSDN Magazine Issues / 2009 / Февраль](https://learn.microsoft.com/ru-ru/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)**
<br>
<br>
*Предметная область (или бизнес-область, сфера бизнеса, business domain) определяет общую сферу деятельности компании. В общем смысле, это услуга, которую компания предоставляет своим клиентам.*
<br>
*Компания может работать в нескольких предметных областях. Например, Amazon предоставляет как услуги розничной торговли, так и облачные сервисы. Uber — это компания по организации поездок, которая также предоставляет услуги по доставке еды и совместному использованию велосипедов.*
<br>
**[What is Domain-Driven Design? // Анализ предметных областей](https://systems.education/wis-ddd-business-domains)**


*Существуют паттерны предметно-ориентированного проектирования, которые определяют способы интеграции и отношений между ограниченными контекстами. Эти паттерны определяются исходя из типа взаимодействия между командами, которые работают над ограниченными контекстами. Мы разделим паттерны на три группы, каждая из которых представляет тип командного взаимодействия: сотрудничество, заказчик-поставщик и раздельные пути.*
<br>
<img src="context_integrations_patterns.png" alt="context_integrations_patterns" width="400"/>
<br>
**[What is Domain-Driven Design? // Сопоставление контекстов](https://systems.education/wis-ddd-context-mapping)**



### Ограниченный контекст
Нужно разделить единый язык на несколько языков поменьше, а затем каждый из них привязать к явному контексту, в котором он может быть применен — его ограниченному контексту. В каком-то смысле конфликты терминологии и неявные контексты являются неотъемлемой частью любого крупного бизнеса. С использованием паттерна ограниченного контекста, они моделируются как явная и неотъемлемая часть предметной области.
