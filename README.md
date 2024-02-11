# Шпаргалка по изученному материалу по Git
Краткий конспект по материалу из Яндекс.Практикума



## Git для Windows
Для работы с __Git__ в _ОС Windows_ используется программа ```GitBash```, которая реализует командную строку ОС UNIX и вместе с тем устанавливает и сам __Git__. <br>
Ссылка на установку есть на официальном сайте [Git](https://git-scm.com).



## Консоль GitBash
```GitBash``` реализует в себе команды Unix-подобных систем, которые, соответственно, сильно отличаются от _ОС Windows_.<br>
Основные команды для работы с файлами:
* ```pwd``` - путь до текущего каталога
* ```ls``` - содержимое текущего каталога. Ключ ```-l``` выводит содержимое в виде списка, ключ ```-a``` отображает скрытые файлы
* ```cd``` - перемещение по каталогам
* ```mkdir```, ```touch``` - создание папки и файла соответственно
* ```cp```, ```mv``` - копирование и перемещение файлов соответственно
* ```rmdir```, ```rm``` - для удаления папки и файла соответственно. Для удаления папок с файлами используется ```rm -r```
> Стоит также упомянуть, что уже введённые ранее команды можно извлекать из буфера стрелками вверх и вниз, а также дописывать команды автоматически, нажимая клавишу __Tab__, после ввода части команды. Для применения любой команды надо нажать __Enter__



## Работа с Git
Чтобы проверить, установлен ли __Git__ используется команда ```git version```. Если установлен, то будет выведена версия ПО.

Перед началом работы __Git__ необходимо настроить, введя как минимум имя пользователя и почту, которые будут указывать, кто произвёл изменения в проекте с __Git__.
Для этого используются команды:
- ```git config --global user.name <Имя пользователя>```
- ```git config --global user.email <Электронная почта>```<br>
Проверить, что изменения сохранены можно командами ```cat ~/.gitconfig``` или ```git config --list```, которые позволяют увидеть содержимое файла настроек __Git__.

Чтобы начать использовать __Git__ в своём проекте, после его создания, находясь в корневой папке проекта, используется команда ```git init``` (init - initialize), которая создаст внутри скрытую по умолчанию папку ```.git```, в которой будет находиться вся информация __Git__.

Чтобы проверить текущее состояние проекта, т.е. отобразить, какие произведены изменения, используется команда ```git status```.
Для сохранения изменений в __Git__ используются коммиты, которые и сохраняют изменения, но прежде, чем создать коммит, необходимо выбрать файл или папку, которую необходимо сохранить. Чтобы начать отслеживать и выбрать файл, используется команда ```git add <имя файла>``` или ```git add --all``` (для отслеживания сразу всех файлов в текущем репозитории). Можно "добавлять в репозиторий" и отдельно текущую папку со всеми файлами, используя ```git add .```.<br>
Теперь необходимо сохранить сами изменения выбранных через ```git add``` файлов, для этого используется команда ```git commit -m 'Сообщение коммита'```. Ключ ```-m``` (message) используется для добавления комментария к коммиту. Чтобы увидеть список всех коммитов, можно использовать команду ```git log```.
> Причём после вывода на экран ```git log``` в самом верху будут отображены самые последние коммиты. Т.е. сверху-вниз список идёт от самых новых к самым старым.
> В каждом коммите будет отображён его идентификатор, автор, дата изменения и комментарий, если он есть.



## Знакомство с GitHub

__GitHub__ - популярная платформа для хранения IT-проектов и совместной работы на ними с использованием Git (_Hub_ с англ. _"узловая станция"_). Платформа позволяет создавать проекты разных типов:
* приватные (видны только создателю)
* командные (видны только членам команды)
* публичные (видны всем)
<br>
Также можно подключаться и к чужим _open source_ проектам и работать над ним вместе с другими людьми со всего мира.


### Разница между Git и GitHub
__Git__ - консольный инструмент для работы с локальными и удалёнными репозиториями, проект с открытым исходным кодом, в то время как __GitHub__ - платформа для размещения удалённых репозиториев, принадлежащая компании _Microsoft_.


Существуют и другие платформы, помимо __GitHub__: __Bitbucket__, __GitLab__ и другие.



## Работа с удалёнными репозиториями GitHub
Для удобного доступа к удалённым репозиториям следует сгенерировать ```SSH-ключ``` при помощи ```ssh-keygen -t ed25519 "Почта аккаунта на GitHub"``` или ```ssh-keygen -t rsa 0b 4090 "почта"```, если при первом способе отобразилась ошибка, т.е. система, скорее всего, не поддерживает алгоритм шифрования ```ed25519```.<br>
Будет создана пара ключей: публичный и приватный, проверить их наличие можно командой ```ls -a ~/.ssh```, которая отобразит содержимое скрытой папки ```.ssh```. Публичный ключ будет с расширением ```.pub```, а приватный без. 
>Приватный ключ нельзя никому передавать, т.к. идея в том, что приватный ключ служит для дешифровки данных при получении, а публичный для шифрования при обращении к серверу.


После генерации публичный ключ можно добавить в свой аккаунт __GitHub__ в его настройках. Проверить правильность ключа после добавления можно при помощи команды ```ssh -T git@github.com```. Если всё верно, будет получено сообщение, что аккаунт успешно аутентифицирован.


Теперь нам необходимо привязать удалённый репозиторий к локальному. Подробная инструкция с командами о том, как это сделать отображается на __GitHub__ при создании репозитория: после нажатия на кнопку, будет предложено создать новый локальный репозиторий, привязать существующий или импортировать код из другого репозитория. Для привязки нам необходимо выполнить код из второго пункта: ```…or push an existing repository from the command line```. <br>
Убедиться, что репозитории связаны, можно командной ```git remote -v```, которая выведет подобный результат:
```bash
$ git remove -v
origin      git@github.com:%АККАУНТ%/%ПРОЕКТ%.git (fetch)
origin      git@github.com:%АККАУНТ%/%ПРОЕКТ%.git (push)
```


Сами по себе коммиты хранятся в ветках, которые представляют собой что-то вроде временных шкал, на которых располагаются изменения. Так несколько веток - несколько параллельных историй изменения кода, которые могут соединяться друг с другом. Как правило, основная ветка называется ```main``` или ```master```_(стар.)_. Чтобы отправить созданные коммиты (изменения) на удалённый репозиторий используется команда ```git push```.


Часто в удалённых репозиториях существует файл ```README.md```, который отображает в себе название проекта, его описание и прочую информацию о нём. Таковым является и данный файл.<br>
```README.md``` использует язык разметки ```markdown```, при помощи которого и оформлен данный документ.


#### На этом всё!
![Спасибо за внимание!](end.jpg)


