<d>
      <details>
            <summary> how I wrote value / Как я записываю переменные </summary>

RUS           
==
            
```html
<пример> - сам пример не содержит знаков <>
```    
Например:
```html
      mysql -u <mysql_пользователь> -p -d <mysql_БД> < <пример>.sql
```
выглядит как:
```vim
      mysql -u root -p -d inno_DB < inno.sql
```
если пример в шаблоне будет в знаках
```python
<> , то экранирую между знаками долларов $....$
```
Например:
```python
      $<пример>$
```

**[OPTIONS]** содержит болле чем одну команду или ключ

ENG
==

```html
<example> - looks likke example without characters <>
``` 
 For example:
 ```html
      mysql -u <mysql_user> -p -d <mysql_database> < <example>.sql
```
looks like:
```vim
      mysql -u root -p -d inno_DB < inno.sql
```
if example have symbols character
```python
<> then i will to escape between dollars character $....$
```
 For example:
```python
      $<example>$
```

**[OPTIONS]** contains more then one command or special key

</details>
</d>

<d>
      <details>
            <summary> Особые символьные тэги в конфигурационном файле /
                      Special symbolic hashtag in config file 
            </summary>
            

    
| ***hashtag*** | ***additional comment*** | ***Decsription*** |
|---|---|---|
|***|<b>On Start String<b>|***|
| | | | | | 
| <b>#M</b> | - commented text | значит я намерено закоментил | 
| <b>#W</b> | - описание\| text | warning |
| <b>#DW</b> | - описание\| text | does work +(text)?| |
| <b>#Er</b> or <b>#ER</b> | - описание\| text | error |
| <b>#R</b> | - описание\| text | removed in version or other |
| <b>#Ed</b> or <b>#E</b> | - описание\| text | eddit |
| <b>#tt</b> or <b>#TT</b> or <b>#T</b> | - описание\| text | test команда для проверки |
||| 
| <b>#!NW</b> | - описание\| text | not work |
| <b>#!NE</b> | - описание\| text | not exist |
| <b>#!WW</b> | - описание\| text | work wrong |
| <b>#!D</b> | - описание\| text | deprecated in verion or other |
| | | | | |
|***|<b>On all other place in string<b>|***|
| | | | 
| <b>#F</b> | - text | формат ввода |
| <b>#V</b> | - text | один из вариантов комманды |
| <b>#C</b> | - comment | комментарий ввиде описания |

</details
</d>
