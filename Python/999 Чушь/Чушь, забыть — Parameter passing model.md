
Как работает присваивание в *Python*?

Простое и множественное присваивание в *Python* работают одинаково. Не умаляя общности можно считать, что 
- слева от знака присваивания всегда стоит кортеж переменных
- справа от знака присваивания всегда стоит кортеж значений

``` Python
x = 0

x, y, z = 0, 1, 2

x, y, z = (0, 1, 2)

x, y, z = (a, y+1, z+2)

(x, y, z) = (x, x+1, x+2)
```

Присваивание работает в три этапа.

Этап 1
Последовательно вычисляются значения из правого кортежа.
Резолвинг имён переменных происходит динамически: L → E → G → B

Если не удаётся разрезолвить имя какой-либо переменной, пользователь получает сообщение об ошибке.  

Этап 2
Последовательно резолвятся имена переменных из левого кортежа.
Резолвинг имён переменных происходит динамически: L → E → G → B

Если не удаётся разрезолвить имя какой-либо переменной, пользователь получает сообщение об ошибке.  

Этап3
Если размеры двух кортежей совпадают, то $i$-й переменной — $i$-му элементу левого кортежа — присваивается ссылка, являющаяся $i$-м элементом правого кортежа.

Если размеры двух кортежей не совпадают, то пользователь получает сообщение об ошибке.

*N.B.*
Каждая область видимости — это структура данных, которая ведёт себя как словарь `dict[str, object]` — ключами этого словаря являются строки — имена переменных, а значениями — ссылки на объекты. 

Таким образом, динамический резолвинг имён переменных — это последовательный поиск значения по заданному ключу в одном из четырёх словарей.


Пример 1

``` Python
x = 0
x, x, x = (x, x+1, x+2)
print(x)

# stdout: 2
```

Пример 2

``` Python
def foo(x):
    x = x + 5

x = 3
foo(x)
print(x)

# stdout: 3
```

1\.
В области видимости *Global* создаётся переменная с именем *x*, значением которой является ссылка на объект числа 3 — заранее созданный и закэшированный на этапе запуска виртуальной машины *Python*.

2\.
При вызове функции *foo* — как и при вызове любой функции — *Python* создаёт новую временную область видимости переменных. И до тех пор, пока функция *foo* находится на вершине стека функциональных вызовов, именно эта область видимости переменных будет выполнять роль области видимости *Local* при динамическом резолвинге имён переменных .

3\.
В области видимости *Local* — в области видимости функции *foo* — находится переменная с именем *x*.

В области видимости *Global* также находится переменная с именем *x*.

Более того, значения этих двух переменных совпадают, так как обе эти переменные ссылаются на один и тот же объект числа $3$.

4\.
При выполнении присваивания `x = x + 5` произойдёт
- динамический резолвинг имени *x* в правой части присваивания
- динамический резолвинг имени *x* в левой части присваивания

В результате обоим именам *x* будет сопоставлена ссылка на один и тот же объект, хранящаяся по ключу *x* в словаре — области видимости — Local. 


???

x = 42

def foo():
    x += 1

foo()
print(x)


???
x = 42

def foo():
    print(x)
    x = 1

foo()
print(x)




Я был единственным тестером большой электронной системы, разработанной для оптимизации взаимодействия отдела продаж с клиентами, на основе моделей предсказания их поведения.  



// Дана строка, содержащая слова, разделённые одиночными пробелами.  
// Нужно написать функцию, которая вернёт строку, где каждое слово заменено на слово, состоящее из тех же букв, но в обратном порядке.  
// Если слово является палиндромом (читается одинаково в обе стороны), его нужно оставить без изменений.  

// "Hello worlD ollo" =>  "olleH Dlrow ollo"
// "привет мир ара", "тевирп рим ара"
// "Hello worlD ollO" =>  "olleH Dlrow ollO"




def is_palyndrome(word):
    return word.lower() == word.lower()[::-1]

def reverse_word(word):
    if is_palyndrome(word):
        return word

    return word[::-1]

def my_function(s: str) -> str:
    return " ".join(map(reverse_word, filter(None, s.split(" "))))


#  
def decorator_with_args(param1, param2):
    def actual_decorator(func):
        def wrapper(*args, **kwargs):
            print(f"Параметры декоратора: {param1}, {param2}")
            result = func(*args, **kwargs)
            return result
        return wrapper
    return actual_decorator

@decorator_with_args("hello", 10)
def say(message):
    print(message)


decorator_with_args("hello", 10)(say)("Hi!")

#
nope = lambda: pass
riser = lambda x: raise Exception(x)

#
print(object() == object())


#
try:
    return 1
finally:
    return 2

#
class D:          attr = 3      #  D:3   E:2
class B(D)        pass          #   |     |
class E:          attr = 2      #   B    C:1
class C(E):       attr = 1      #    /   /
class A(B, C):    pass          #      A
X = A()                         #      |
print(X.attr)                   #      X

# DFLR = [X, A, B, D, C, E]
# MRO = [X, A, B, D, C, E, object]



#
class D:          attr = 3      #  D:3   D:3
class B(D)        pass          #   |     |
class C(D):       attr = 1      #   B    C:1
class A(B, C):    pass          #    /   /
X = A()                         #      A
print(X.attr)                   #      |
                                #      X


#



CREATE TABLE customer
(
    id      INTEGER PRIMARY KEY,
    email   VARCHAR(100)    NOT NULL,
    country CHAR(2)         NOT NULL
);

CREATE TABLE cart_item
(
    id          INTEGER PRIMARY KEY,
    customer_id INTEGER         NOT NULL,
    title       VARCHAR(20)     NOT NULL,
    amount      INTEGER         NOT NULL,
    price       INTEGER         NOT NULL    
);



customer
--------
1, c1@example.com, ru
2, c2@example.com, ru
3, c3@example.com, ru
4, c4@example.com, by

cart_item
---------
1,  1, пиво,    6, 100
2,  1, вода,    2,  50
3,  2, печенье, 1,  75
4,  2, сок,     2,  60

--- Интересуют только покупатели(id, email, сумму корзины) из России, которые положили в корзину товаров не менее чем на 1000 рублей


select c.id, c.email, sum(ci.amount * ci.price)
from customer c inner join cart_item ci on c.id = ci.customer_id
where c.country = 'ru'
group by c.customer_id, c.email
having sum(coalesce(ci.amount, 0) * ci.price) >= 1000


SOLID

ACID
4 уровня изолированности транзакций

Виды индексов

#
Вот у нас таблица ид, имя и email

И что делать есть нам часто надо выбирать по части после @
По mail.ru, gmail.com и прочее


# USD, 10
  USD, 20
  USD, 15



#

"""
Load Balancer

Stage 1
Register instances

It should be possible to register an instance, identified by an address

Each address should be unique, it should not be possible to register the same address more than once 

Load Balancer should accept up to 10 addresses

input data - IP - str


Stage 2
Random invocation 

Develop an algorithm that, when invoking the Load Balancer 's get() method multiple times, \
    should return one backend-instance choosing between the registered ones randomly.
"""



  


