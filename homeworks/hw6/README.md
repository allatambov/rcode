Домашнее задание 6
================
Алла Тамбовцева

Формат сдачи
------------

*Срок сдачи:*

12 декабря 2017, 22:00

*Формат сдачи:*

Результат выполнения домашнего задания 6: файл с расширением `.R`. Этот файл нужно загрузить по [ссылке](https://www.dropbox.com/request/gRSzGjPot9knhcxw3lmD). 


В этот раз задания общие для обоих блоков (базовый, продвинутый).

**Задание 1**

В этом задании вам предлагается поработать с базами данных, в которых сохранена информация о том, как называли детей в 2015--2017 годах (детализация по месяцам). Вам предложены две базы данных (`boys.csv` и `girls.csv`), содержащие следующие переменные:

* Name -- имя

* NumberOfPersons -- число детей, названных этим именем

* Year -- год

* Month -- месяц

Данные взяты с [OpenData]().

1. Загрузите базы данных `boys.csv` и `girls.csv`, посмотрите на них. Обратите внимание на кодировку и разделитель столбцов + считайте, что текстовые переменные должны считываться R как текст, а не как факторы (аргумент `stringsAsFactors`).

2. Используя библиотеку `dplyr`, создайте в базах имен столбец `gender` (тип factor), все значения которого равны "M" (для базы имен мальчиков) или "F" (для базы имен девочек). Итог: в обеих базах есть одинаковый столбец `gender`, состоящий либо из повторяющихся нужное число раз букв "M" или "F".

3. Соедините две базы имен по строкам (все столбцы одинаковы, просто к первой базе приписываем все строки второй базы) и сохраните результат в переменную `total`. *Подсказка:* функция `rbind()`.

4.  Даны два вектора имен:

```
G <- c("Анастасия", "Валентина", "Дарья", "Евгения", "Елизавета",  "Ирина", "Камила", "Полина",  "Светлана", "Юлия")
B <- c("Андрей", "Артём", "Александр", "Всеволод", "Даниил", "Денис", "Игорь", "Илья", "Кирилл", "Никита", "Сергей")
```

Выберите из базы данных `total` только эти имена, сохраните результат в переменную `small`.

5. В этом задании вам нужно будет визуализировать популярность имен в течение двух лет (по месяцам). Для построения линейного графика (line plot) вам потребуется создать временную шкалу -- склеить и преобразовать столбцы `Year` и `Month`: 

```
library(zoo) # для функции as.yearmon()
small <- small %>% mutate(date = paste(Year, Month, sep = "-"))
small <- small %>% mutate(date = as.Date(as.yearmon(date, "%Y-%b")))
```

Если библиотека `zoo` не установлена, установите ее. Создайте столбец `date`, используя код выше. Посмотрите на него внимательно, определите его тип.

6. Постройте с помощью библиотеки `ggplot2` линейный график (*line plot*), такой, чтобы по нему можно было определить динамику популярности имен девочек и мальчиков (временную шкалу мы уже создали в `date`). При этом постройте графики для женских и мужских имен в отдельных ячейках. Сделайте линии, соответствующие разным именам, разного цвета (более контрастно, чем цвета R по умолчанию, потому что радужный спектр R не всегда позволяет увидеть различия в похожих цветах). Дайте название графику. 

*Подсказка:* без всяких оформительских настроек (цветов и подписей к осям) график на этом этапе должен выглядеть примерно так: []().

 * Поправьте шкалу по оси `x` таким образом, чтобы на оси были отметки времени через каждые 6 месяцев (см. help для слоя `scale_x_date`), причем формат даты должен быть такой: "01-2015", то есть "номер месяца-год полностью". 

    *Подсказка:* чтобы понять, каким образом выставить нужный формат даты, поиграйте с аргументом `date_labels` внутри `scale_x_date`. Другими словами, поподставляйте разные варианты: "%m-%y", "%m-%Y", "%b-%y", "%b-%Y". И определите, что вам подходит.

 * Поверните подписи на оси `x` на 60 градусов, чтобы даты не накладывались друг на друга. 

    *Подсказка:* слой `theme()` и аргумент `axis.text.x = element_text()` в нем. 

**Задание 2**

На основе [отчета Deloitte](https://www2.deloitte.com/ru/en/pages/consumer-business/articles/2016/new-year-spending-survey-2017.html) о потребительских расходах в зимние праздники 2017, была составлена база данных `ny_gifts.csv`. Описание переменных:

* gift: подарок, который потребители хотят получить/покупают другим (тип `character`)

* perc: процент потребителей, которые хотят получить этот подарок/покупают другим (тип `numeric`)

* type: тип подарка, dream -- потребители желают получить, real -- потребители покупают (тип `factor`)

* both: тип подарка, 0 -- либо потребители хотят его получить, либо покупают сами, 1 -- хотят получить и покупают сами (тип `factor`)

*Пояснение:* в базе данных есть две строки 

```
[gift perc type both]
[Money 67 dream 1]
[Money 32 real 1]
```

Это означает, что 67% респондентов сказали, что хотели бы получить деньги на Новый год, а 32% респондентов сказали, что дарят деньги на Новый год. 


В базе данных есть одна строка:

```
[gift perc type both]
[Cooking accessories 18 real 0]
``` 

Это означает, что 18% респондентов сказали, что они покупают кухонные принадлежности в подарок, а какой-то маленький процент респондентов мечтает получить кухонные принадлежности в подарок (такой маленький, что его нет в отчете). Здесь `both = 0`: такой подарок дарят, но не очень хотят получать.

Постройте с помощью `ggplot2` парную столбиковую диаграмму, такую, чтобы по ней можно было сравнить, сколько процентов людей хотели получить какие-то вещи на Новый год, с тем, сколько процентов людей покупают эти же вещи в подарок на Новый год. Примеры парных столбиковых диаграмм -- см. на с.18 или с.23 отчета Deloitte.

*Указания:*

* Оставьте в базе только те подарки, которые потребители одновременно хотят получить и покупают сами.

* Для того, чтобы значения в столбце `perc` воспринимались как уже готовые частоты (проценты), в `geom_bar()` нужно выставить параметр `stat = "identity"`. Иначе R будет считать частоты "заново", то есть определять, сколько в столбце значений 67, 32 и так далее.

* Полезная [ссылка](http://www.sthda.com/english/wiki/ggplot2-barplots-quick-start-guide-r-software-and-data-visualization) про столбиковые диаграммы. Обратите внимание на *dodged barplot*. 