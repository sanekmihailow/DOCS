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

</details>
</d>
