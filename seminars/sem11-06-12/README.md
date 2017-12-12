# Семинар 11. Географические карты в R.

*06 декабря 2017*

1. Загрузите shape-файлы для Соединенных Штатов Америки с сайта [Global Administrative Areas](http://www.gadm.org/country). Постройте карту США (пока пустую). Уберите из shp-файла Аляску и Гавайские острова. Постройте карту еще раз. Сравните.

2. Загрузите базу данных `states.csv`, в которой хранятся показатели по округам (counties) США. В задании нас будет интересовать раскраска карты штатов в соответствии с численностью населения в них (данные за 2010 год, `popul10`). Сгруппируйте значения в базе данных по штатам по этому показателю и сохраните результат в базу `data`.

3. Раскрасьте карту США в соответствии с численностью населения. Выберите любую палитру цветов, считайте, что мы хотим разбить значения численности населения на 9 групп (по процентилям).