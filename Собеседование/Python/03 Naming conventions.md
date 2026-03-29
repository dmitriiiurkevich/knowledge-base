
### Identifier Names

Identifier names
- case-sensitive
- must follow certain rules
- shall follow certain conventions

Rules:
1. start with underscore or a letter,
2. followed with any number of underscore, letter or digits,
3. can’t be reserved words

Conventions:

1\.
`_my_var` — *internal use indicator* по PEP 8 — переменные класса или экземпляра класса, названные так, не предназначены для использования вне класса, в котором они объявлены.

Названные таким образом объекты не будут импортированы выражением

``` python
from my_module import *
``` 

если только эти объекты не будут явно добавлены в коллекцию `__all__`, определённую в файле `__init__.py` модуля  `my_module`.


2\.
`__my_var` — *class private* — интерпретатор автоматически заменяет такие имена на имена вида `_myclassname__my_var`. Что позволяет избежать перекрывания имён атрибутов класса при наследовании.
  
  
3\.
 `__my_var__` – такие имена используются разработчикам Python для именования системных (магических) методов и переменных. Не следует называть свои методы и переменные таким образом, иначе в какой-нибудь из будущих версия Python может случиться конфликта имён.


### Другие PEP 8 naming conventions  

Packages:
short all lowercase names, preferably no underscores

Modules:
short all lowercase names, can have underscores

Classes:
upper camel case convention

Functions:
lower snake case

Variables:
lower snake case

Constants:
all uppercase, underscore separated


“A foolish consistency is the hobgoblin of little minds, adored by little statesmen and philosophers and divines.” — Ralph Waldo Emerson