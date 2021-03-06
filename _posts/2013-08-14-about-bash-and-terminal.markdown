---
layout: post
title:  "О bash и терминале"
date:   2013-08-14 00:00:00
tags: linux, *nix, terminal, bash
---
# Вместо введения

Этот сайт создается как попытка собрать материалы, интересные новичку в мире [*nix][unix-like]. Планирую написать пару-тройку небольших и, по возможности, простых обзорных статей, в основном, о Linux в формате "почитать и переварить за 5-10 минут". Хотя насчёт точности изложения я не ручаюсь, надеюсь кому-то это пригодится ;) Напоминаю, что перед тем, как что-то делать на компьютере, нужно думать.  
Поехали!

***

## Разделяй и властвуй

Unix-подобные системы (Linux, OS X и др.) состоят из большого количества простых программ, каждая из которых выполняет одну функцию. Если нужно выполнить какое-то достаточно сложное действие, комбинируют нескольких программ. Чаще всего это происходит незаметно для пользователя, но почему бы не научиться пользоваться этим универсальным методом? Ведь команды можно записать в файл в нужной последовательности -- так называемый сценарий, или shell script -- и пользоваться этим сценарием каждый раз. Идея в том, что задача разбивается на простые подзадачи, для которых есть готовые инструменты в системе. Есть один кажущийся недостаток: нужно знать, какой набор программ в них входит. Кажущийся, потому что чем больше узнаёшь, тем проще найти подходящий инструмент для выполнения задачи и тем больше времени можно сэкономить в ближайшем будущем, ускоряя рутинные действия. В Linux, безусловно, есть GUI (графический интерфейс пользователя) и мышь, но часто проще открыть окно терминала и ввести несколько простых команд, чем кликать мышью.  

## Взгляд на bash с высоты пингвиньего полета

Для начала надо немного освоиться в терминологии. Сегодня мы познакомимся с [эмулятором терминала][terminal] и [bash](http://ru.wikipedia.org/wiki/Bash).  
Эмулятор терминала -- это программа, которая выполняет функции терминала компьютера (это физическое устройство когда-то использовалось для взаимодействия пользователей с компьютером). Говоря проще, это окно, в котором запущен интерпретатор команд bash или любой другой. Примеры таких программ в *nix:  
`xterm` -- стандартный эмулятор терминала для X Window System (оконной системы). Его можно найти в большинстве дистрибутивов Linux.  
`Konsole` -- эмулятор в среде KDE  
`GNOME Terminal` -- эмулятор в среде GNOME  
`Terminal.app` -- эмулятор в OS X.

Обычно мы используем окно терминала для работы с [командной оболочкой](http://ru.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BD%D0%B0%D1%8F_%D0%BE%D0%B1%D0%BE%D0%BB%D0%BE%D1%87%D0%BA%D0%B0_UNIX) [bash](http://ru.wikipedia.org/wiki/Bash). `bash` -- это программа, которая интерпретирует команды пользователя, а эмулятор терминала отображает ввод и вывод этих команд в своем окне. В Линуксе можно запустить терминал, выбрав в меню KDE программу Konsole или в Gnome программу GNOME Terminal, или попробовать вызвать окно быстрого запуска, нажав Alt + F2 и введя konsole или gnome-terminal, или xterm в строке ввода. Что-то из этого должно сработать.  
Примеры команд, которые можно прямо сейчас выполнить в окошке терминала:

{% highlight bash %}
# Завершить процесс skype
# Здесь sudo означает запустить с правами суперпользователя
# killall -SIGKILL skype означает послать сигнал KILL процессу. 
# Этот сигнал завершает приложение.
$ sudo killall -SIGKILL skype

# Узнать путь, по которому установлена программа xterm
$ whereis xterm

# Прочитать справочное руководство программы whereis. 
# В режиме просмотра доступны следующие команды:
# *Выйти из справки - q;
# *Листать вниз - PageDown или f
# *Листать вверх - PageUp или b
# *Искать слово - /
$ man whereis

# Справка по команде man
$ man man 

# Перейти в домашний каталог пользователя
$ cd

# Перейти в домашний каталог, указав путь к нему ~ явно 
$ cd ~

# Перейти в корневой каталог /
$ cd /

# Перейти в каталог хранения врЕменных файлов /tmp
$ cd /tmp

# Вывести текущий каталог
$ pwd

# Вывести содержимое текущего каталога.
$ ls

# Вывести содержимое каталога ~, включая "скрытые" файлы
$ ls -al ~
{% endhighlight %}

Окно терминала с запущенным `bash` выглядит примерно так:  
![Screenshot]({{ site.url }}/images/terminal.png)  
или так  
![Screenshot]({{ site.url }}/images/bash_screenshot.png)  

Обычно приглашение ввода команд имеет примерно такой вид:  
`hostname:~ username$ `.  
Здесь:  
`hostname` -- имя компьютера;  
`~` -- путь к текущему каталогу (тильда означает, что текущий каталог -- домашний каталог пользователя);  
`username` -- имя пользователя.

Знаком `$` обозначено приглашение для ввода команд в окне терминала. Если команда должна быть запущена с привилегиями root (администратора), вместо `$` используют знак `#` и приглашение выглядит примерно так:  
`hostname:/ root# `.

В завершение обзора привожу полезные ссылки:

- Журнал [LinuxFormat](http://wiki.linuxformat.ru/index.php/%D0%97%D0%B0%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%B0%D1%8F_%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0) по-русски. Много интересных статей. Советую.

- С [bash](http://ru.wikipedia.org/wiki/Bash) можно знакомиться постепенно.

- В статье [Искусство программирования на языке сценариев командной оболочки](http://rus-linux.net/MyLDP/BOOKS/abs-guide/flat/abs-book.html) приводится много полезных примеров использования сценариев.

- Рецепты по решению разнообразных задач можно найти в [Настольной книге по Linux](http://ru.wikibooks.org/wiki/Linux-hand-book).

Список ссылок постараюсь пополнять.  

[unix-like]: http://ru.wikipedia.org/wiki/UNIX-%D0%BF%D0%BE%D0%B4%D0%BE%D0%B1%D0%BD%D0%B0%D1%8F_%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0
[terminal]: http://ru.wikipedia.org/wiki/%D0%AD%D0%BC%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80_%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D0%B0%D0%BB%D0%B0