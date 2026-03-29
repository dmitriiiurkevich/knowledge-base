
`$ sudo apt install -y make`

Мейк-файл — это набор инструкций для программы *make*. Предположим, что в текущей директории есть файл *Makefile* со следующим содержимым:

```shell 
my_target:
	echo "Hello, world!"
```


`$ make my_trget`

Эта команда
- найдёт в текущей директории файл с именем *Makefile*, 
- найдёт в этом файле цель с именем *my_target*, 
- запустит набор команд, соответствующий цели *my_target*, в данном случае, — единственную команду `echo "Hello, world!"`.

Отступы в мейк-файлах задаются только символами табуляции.

Есть возможность [передачи парамтров](https://chriswiegman.com/2021/08/using-parameters-in-a-make-target/).

## Зависимости между целями

Цели могут ссылаться на другие цели.

```shell 
my_target:
	echo "Hello, world!"
	
my_other_target: my_target
	echo "Bye!"
	
```

Цель *my_target* будет запущена перед запуском цели *my_other_target*.

## Инструкция *phony*

```shell 
.PHONY: my_target
my_target:
	echo "Hello, world!"
```

Если имя цели совпадёт с именем одного из файлов в текущей директории, использование инструкции *phony* позволит разрешить возникший конфликт имён: одноимённый файл будет проигнорирован.

## Комментарии

```shell 
# Greet the user
.PHONY: my_target
my_target:
	echo "Hello, world!"
```



