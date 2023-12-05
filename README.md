# CONCAT_YOUR_EXCELS
### Назначение:
Программа позволяет быстро объединять в одну таблицу большое количество экселевских таблиц "раскиданных" в разных экселевских книгах на разных листах.
Заголовки таблиц могут располагаться в разных строках (где-то, например, на третьей строке, а где-то на пятой) и начинаться с разных колонок. Названия колонок могут иметь разный порядок. Значения колонок с одинаковыми названиями попадают в одну колонку итоговой таблицы.
Пользователь может выбрать листы в книгах Эксель, таблицы с которых должны быть объединены.
Программа позволяет объединить экселевские файлы быстрее (примерно в 10 раз) и удобнее чем средствами Power Query. Так же программа показывает прогресс обработки, что не возможно реализовать используя Power Query.
Результат выгружается в CSV-файл, так как итоговая таблица может иметь количество строк превышающее допустимое в Эксель.
Из итогового результата автоматически вычищаются строки и колонки не имеющие значений.

---
### Как пользоваться:
1. Настройте Эксель (настройка требуется один раз). Для этого выберете: **Данные => Получить данные => Параметры запроса => Конфиденциальность => Глобальные => Всегда игнорировать параметры уровней конфиденциальности**.
2. Создайте папку проекта.
3. В папке проекта создайте папку **Исходники**. В папку **Исходники** поместите экселевские файлы таблицы на листах которых должны быть объединены. Экселевские файлы могут располагаться как непосредственно в самой папке **Исходники**, так и во вложенных папках (допускается любой уровень вложенности).
4. Скопируйте в папку проекта файлы:
-  **.headers.xlsx**
-  **.sheets.xlsx**
-  **.statistics.xlsx**
-  **CONCAT_YOUR_EXCELS.exe** (для создания файла используйте скрипт **auto-py-to-exe** с настройками: **One File, Console Based**).
5. Запустите программу **CONCAT_YOUR_EXCELS.exe**. Откроется окно консоли через которое будет осуществляться информирование о ходе выполнения обработки. Программа просканирует листы в книгах в папке **Исходники**. Откроется **Управляющее окно** с кнопками **Просмотреть листы** и **Собрать заголовки**. Откроется книга Эксель **.sheets.xlsx**. На листе **Sheets_in_book** этой книги в столбце **Добавить** оставьте пустые значения для листов, таблицы с которых не нужно будет объединять, или введите "ДА" (большими буквами) для листов, таблицы с которых нужно будет объединить. <br>_**Будьте аккуратны, если Вы случайно поменяете названия столбцов в этой таблице, программа может работать неправильно!**<br>_ Если какие-либо таблицы содержат больше строк или столбцов, чем нужно загрузить, в колонках **Сколько строк нужно** и **Сколько колонок нужно** книги **.sheets.xlsx** укажите необходимые значения. Обратите внимание на листы, значения в колонках **Строк на листе** и **Столбцов на листе** для которых имеют значения резко отличающиеся от аналогичных значений для других листов. Скорее всего книги содержащие эти листы нужно открыть в Экселе, просмотреть "подозрительные" листы и принять решение: сколько строк и листов нужно сканировать. Лишние столбцы и строки могут замедлять выполнение программы. Слишком большие таблицы (количество строк в которых приближается к 1'000'000, а столбцов к 16'000) могут не поместиться в оперативной памяти и остаться не обработанными. Сохраните и закройте книгу **.sheets.xlsx**.
6. Нажмите кнопку **Собрать заголовки** в **Управляющем окне**. Для ускорения обработки заголовки ищутся в фрагменте 30 строк на 30 колонок (превью). Программа загрузит в оперативную память информацию с отобранных листов. Откроется книга **.headers.xlsx**. На вкладке **Not located** этой книги отобразится превью таблицы с листа отобранного для добавления для которого нужно найти признак по которому можно идентефицировать заголовок (например для тестового примера это колонка 0 значение "А"). Перейдите на вкладку **Settings** и внесите в таблицу признак заголовка. Закройте книгу **.headers.xlsx** и нажмите кнопку **Собрать заголовки**. Программа вновь просканирует листы. В окне консоли отоборазится информация для каких листов заголовки найдены, а для каких нет. Вновь откроется книга **.headers.xlsx**. На листе  **Not located** отобразится превью таблицы для которой не удалось найти заголовок по уже отмеченным на листе **Settings** признакам. Примите решение по какому признаку можно найти заголовок для этой таблице и добавьте информацию об этом признаке в таблицу на листе **Settings**. Если по разным признакам будут идентифицированы несколько строк, как строки содержащие заголовки, информация о них отобразится на листе **Multiple headers**.  Примите решение по какому признаку не нужно отбирать заголовки для одной из строк и скопируйте информацию на лист **Exceptions**, чтобы добавить этот признак для данного листа в исключения. Повторяйте процедуру пока не найдете заголовки для всех отобранных листов. Когда заголовки будут найдены для всех отобранных листов, появится кнопка **Объединить таблицы**. Перейдите на лист **Headers** книги **.headers.xlsx**, просмотрите найденные заголовки.
7. Если заголовки собраны корректно, нажмите кнопку **Объединить таблицы**. Объединяются полные таблицы (не превью). Если таблица содержит более одной колонки с уникальным названием, такая таблица не будет добавлена в итоговый результат. Информация о книге и листе с такой таблицей отобразятся в консоли. После окончания объединия, Вы можете открыть в Экселе книгу с листом на котором была обнаружена коллизия и, откорретировав заголовки этой таблицы, заново запустить сбор заголовков и объединение таблиц нажатием соответствующих кнопок **Управляющего окна**. 
Результат выполнения программы будет сохранен в файле **RESULT.csv**
8. Для того, чтобы объединить другие листы экселевских книг из папки **Исходники** в обобщенную таблицу и записать их в файл **RESULT.csv**, не останавливая программу нажмите в **Управляющем окне** кнопку **Просмотреть листы**. Внесите необходимые изменения в столбце **Добавить** открывшейся книги **.sheets.xlsx**, заново соберите заголовки и нажмите кнопку **Объединить**.
9. По мере надобности в папку **Исходники** можно добавлять новые файлы или удалять ненужные. Программу при этом можно не останавливать, что, в случае если поменялись не все файлы, которые необходимо обработать, может заметно ускорить обработку.
---
### Описание алгоритма: