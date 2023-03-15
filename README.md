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