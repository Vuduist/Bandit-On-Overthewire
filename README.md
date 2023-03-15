# Bandit On Overthewire 
Окей, в рамках практики работы с git, по совету ментора, решил описать процесс решения bandit с сайта overthewire.org

### Уровень 0-1
Квест простейший - нужно просто подключиться  по ssh к серверу bandit.labs.overthewire.org от лица пользователя bandit0. 
Это делается следующей командой:
>root$ ssh bandit0@bandit.labs.overthewire.org -p 2220

Хотя лично для меня был удобнее менее каноничный вариант:
>root$ ssh bandit.labs.overthewire.org -p 2220 -l bandit0

Далее необходимо осмотреться, какие файлы есть на сервере. Используем команду ls и получаем следующий результат:
>bandit0@bandit:~$ ls 
>
>readme

Видим всего один нескрытый файл - readme. Смотрим, что внутри:
>bandit0@bandit:~$ cat readme
>
>NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

А вот и пароль! Используем его для подключения к следущему уровню.

### Уровень 1-2
Подключаемся к bandit1
>root$ ssh bandit.labs.overthewire.org -p 2220 -l bandit1
>
>bandit1@bandit.labs.overthewire.org's password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

Пароль к следущему уровню находится в файле "-". Открываем его и получаем ответ:

>bandit1@bandit:~$ cat ./-
>
>rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

И вновь пароль! Переходим к 2-3

### Уровень 2-3

По классике проверяем содержимое директории:
>bandit2@bandit:~$ ls
>
>spaces in this filename

Всего один файл. Смотрим, что внутри:

>bandit2@bandit:~$ cat spaces\ in\ this\ filename
>
>aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

Вновь пароль. Пока просто, но не раслабляемся.

### Уровень 3-4

Смотрим, что есть тут.

>bandit3@bandit:~$ ls
>
>inhere

Как и сказанно в описании задания, нас встречает директория inhere. Переходим в неё и смотрим, что там:

>bandit3@bandit:~$ cd inhere/
>
>bandit3@bandit:~/inhere$ ls

И тишина. Файлы скрыты. Чтобы посмотреть скрытые файлы добавляем опцию -a:

>bandit3@bandit:~/inhere$ ls -a
>
>.  ..  .hidden

А вот и скрытый файл. Смотрим, что там.

>bandit3@bandit:~/inhere$ cat .hidden
>
>2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

Код найден. Идём дальше.

### Уровень 4-5

Ситуация таже - папка inhere, но в ней уже несколько файлов:

>bandit4@bandit:~$ ls
>
>inhere
>
>bandit4@bandit:~$ cd inhere/
>
>bandit4@bandit:~/inhere$ ls
>
>-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

Из описания уровня известно, что пароль находится в одном из человеко-читаемых файлов. Мы, конечно, могли бы  прочесть каждый из файлов cat'ом, но это как-то непрофессионально, поэтому спрашиваем у системы, какого типа эти файлы утилиткой file. Для ускорения процесса используем регулярное выражение "./-*" оно указывает утилите file, что она должна вывести формат файла для каждой позиции, начинающейся со знака тире(-*) из актуальной директории(./) 

>bandit4@bandit:~/inhere$ file ./-*
>
>./-file00: data
>
>./-file01: data
>
>./-file02: data
>
>./-file03: data
>
>./-file04: data
>
>./-file05: Non-ISO extended-ASCII text, with NEL line terminators
>
>./-file06: Non-ISO extended-ASCII text, with no line terminators, with escape sequences
>
>./-file07: ASCII text
>
>./-file08: data
>
>./-file09: data

Среди кучи файлов выделяется один -file07. Открываем его:

>bandit4@bandit:~/inhere$ cat ./-file07
>
>lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

Good job!