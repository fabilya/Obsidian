	![[Pasted image 20230220092649.png]]




**git clone <ссылка на удаленный репозиторий>** - клонирование удаленного репозитория в локальный
**origin** - имя удаленного репозитория по-умолчанию
**git branch -a** - отображает все ветки, включая те, которые находятся в удаленных репозиториях
**git checkout <имя ветки>** - переход в любую ветку, в том числе ветку в удаленном репозитории
**git pull** - загружает и применяет изменения с удаленной ветки в локальную ветку
**git push** - загружает и применяет изменения из локальной ветки в ветку удаленного репозитория

## Связь существующего локального репозитория с удаленным

**git remote add origin <ссылка на удаленный репозиторий>** - подключение удаленного репозитория
**git push -u origin <имя ветки>** - загрузка изменений из локальной ветки в удаленную с созданием связи между ними
**git push** - дальнейшие загрузки изменений в ветку **удаленного** репозитория после установки связи между локальной и удаленной ветками
**git pull** - дальнейшие загрузки изменений в ветку **локального** репозитория после установки связи между удаленной и локальной ветками