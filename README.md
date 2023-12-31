# Regexp

**Regexp** — формальный язык поиска и осуществления манипуляций с подстроками в тексте

Для ограничения начала и конца строки необходимо использовать специальные символы Эти символы не нужны для поиска совпадений с регулярным выражением внутри текста
- ^ — начало строки
- $ — конец строки

Метасимволы, используемые в Regexp
```
- . - Любой символ
- [ ] - Диапазон символов
- [^ ] - Все символы, кроме указанных в фигурных скобках
- * - Любое количество символов перед звёздочкой, в том числе ноль
- + - Одно или несколько стоящих перед ним выражений
- ? - Ноль или одно стоящее перед ним выражение
```
```
^tes.$ = test / tes5
^tes[tl]$ = test / tesl
^tes[a-z]$ = test / tesa
^tes[^t]$ = tesa / tes6   no - test / tes
^test*$ = tes / testtttttttt   no - est
.* = Все
^ab[cd]*$ = abcccdddcdcddd / ab
^ab1+$ = ab111 / ab1
^ab1?$ = ab1 / ab   no - ab11 / ab2
```
**Квантификатор** — указатель количества предшествующих выражений или символов
- Символ * - * = {0,}
- Символ + - + = {1,} 
- Символ ? - ? = {0,1}
- {n} - Непосредственное количество
- {n,} - n или больше
- {n,m} - Не меньше, чем n, и не больше, чем m
- {,m} - Не больше, чем m
```
wa[tr]{2} = watt
tre{1,} = tree
gab{0,1}[em]{1,3} = game
tol{,3} = toll
```

Экранирование и группировка
- Для экранирования в регулярных выражениях используется специальный символ \
- Сам \ экранируется как \\
- Применить квантификатор к нескольким символам сразу можно, использовав группировку: ( )
- В качестве логического ИЛИ можно использовать |
```
^(https?:\/\/)?(www\.)?netology\.[a-z]{2,4}$
^(Москва|Ленинград|Казань)+$
```
**Grep** — утилита для поиска строк, соответствующих регулярному выражению
```
grep -E 'regexp' file
-E — расширенное регулярное выражение (Extended Regexp)
-v — инверсия вывода
-с — подсчёт количества выводимых строк вместо их вывода
-n — вывод номера строки
-i — нечувствительность к регистру
-r — рекурсивный поиск по всем файлам
```

**Stream editor** - Потоковый редактор

**Sed** — потоковый текстовый редактор, применяющий различные предопределённые текстовые преобразования к последовательному потоку текстовых данных
```
sed 's/abc/xyz/g' file > file2
```
Заменяет все строки abc на xyz в файле file и перенаправляет получившийся результат в file2
получившийся результат в .

Или в потоке:
```
echo '123asd123' | sed 's/1/3/g
```
Ключи
- -E — позволяет использовать регулярные выражения в sed
- sed 'pattern/d' — удаляет строки, содержащие символы из pattern
- -i, --in-place — производит замену в изначальном файле file
- Если после ключа указать текст, будет создан бэкап

**Awk** — скриптовый язык, который полезен при работе в командной строке и широко применяется для обработки текста. Обладает практически безграничными возможностями по обработке данных благодаря встроенному языку программирования Данные, поступающие в awk, можно представить в виде таблицы, где строки таблицы — это строки в традиционном понимании, а разделителем столбцов выступает пробел

Столбцы заносятся в переменные:
- $0 — вся строка целиком
- $1 — первый столбец
- $2 — второй столбец
- Чтобы использовать другой разделитель столбцов, можно применить ключ -f

Встроенные переменные
- FS — разделитель столбцов
- RS — разделитель строк
- OFS — выходной разделитель столбцов
- ORS — выходной разделитель строк

Синтаксис
- Вывод чего-либо на экран: print ''
- Объявление переменных: var='value'
- Условный оператор: if-then-else
- Цикл while: while (i > 0){}

Когда awk-скрипт перестаёт помещаться в одну строку, можно поместить его в файл и указать его имя ключом : -f
```
awk -f /tmp/awkscript
```
```
ps aux | awk '{print $2 $8}'
cat /etc/passwd | awk -F: 'BEGIN{OFS=" "} {print $1,$6,$5}'

ps aux | awk '{if ($2 > 2000) print $0}'

cat /proc/loadavg | awk '{i=1; sum=0; while (i<4){ sum += $i; i++ }
print $sum/$i }'

tail access.log
cat access.log | awk '{print $9}' | sort | uniq -c
```
