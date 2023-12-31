# Функціональне програмування в Python

* **Вступ**

  - Визначення функціонального програмування

  - Історія функціонального програмування

  - Переваги та недоліки функціонального підходу

  - Різниця між функціональним та імперативним стилями програмування

* **Основні концепції функціонального програмування**

  - Чисті функції та побічні ефекти

  - Незмінність даних

  - Вищі функції

  - Каррінг та часткове застосування

  - Рекурсія

* **Основи функціонального програмування в Python**

  - Визначення та створення функцій
    - Приклади стандартних функцій
    - Локальні та глобальні змінні

  - Анонімні функції: 
    - `lambda`
    - Приклади застосування `lambda` функцій

* **Вбудовані функції Python**

  - `map()`: Приклади роботи з `map`

  - `filter()`: Фільтрація списку за допомогою `filter`

  - `reduce()`: Агрегація даних з допомогою `reduce`

* **Декоратори**

  - Визначення та основи роботи з декораторами

  - Створення власних декораторів
    - Приклади декораторів для вимірювання часу виконання
    - Декоратори з параметрами

* **Функціональні бібліотеки для Python**

  - `functools`: корисні утиліти для підтримки функціонального стилю

  - `itertools`: ефективна робота з ітераторами



**Вступ**
---

**1. Визначення функціонального програмування**

Функціональне програмування — це парадигма програмування, в основі якої лежить обробка даних за допомогою функцій. В функціональному програмуванні велика увага приділяється незмінності даних та відсутності побічних ефектів при роботі з функціями.

```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # Виведе: 8
```

---

**2. Історія функціонального програмування**

Функціональне програмування бере свій початок від лямбда-ісчислення, математичної теорії, що була створена в 1930-х роках Алонзо Черчем. Мови програмування, як-от Lisp, що з'явилися в 1950-х роках, брали за основу функціональні принципи.

---

**3. Переваги та недоліки функціонального підходу**

*Переваги:*
- **Прозорість:** Функції не мають побічних ефектів, що спрощує розуміння коду.
- **Тестування та налагодження:** Чисті функції легше тестувати, оскільки для одних і тих самих вхідних даних вони завжди повертають один і той же результат.
- **Безпека:** Незмінність даних допомагає уникнути багатох типів помилок.

*Недоліки:*
- **Складність:** Для людей, звиклих до імперативного стилю, може бути важко перейти на функціональний підхід.
- **Продуктивність:** В деяких випадках функціональний код може бути менш ефективним порівняно з імперативним.

---

**4. Різниця між функціональним та імперативним стилями програмування**

*Імперативний стиль:* Основується на командах, які змінюють стан системи. Він деталізує, *як* досягти бажаного результату.

```python
numbers = [1, 2, 3, 4, 5]
squared = []
for num in numbers:
    squared.append(num ** 2)
```

*Функціональний стиль:* Орієнтований на те, *що* потрібно зробити, зосереджуючись на обчисленнях і використанні функцій.

```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
```

У функціональному коді вище ми використовуємо функцію `map`, щоб отримати квадрат кожного числа зі списку `numbers`.



**Основні концепції функціонального програмування**
---

**1. Чисті функції та побічні ефекти**

Чиста функція — це функція, яка повертає значення на основі своїх вхідних параметрів і не має побічних ефектів.

*Приклад чистої функції:*
```python
def add(a, b):
    return a + b
```

*Приклад функції з побічними ефектами:*
```python
x = 10

def add_to_x(y):
    global x
    x += y
    return x
```

---

**2. Незмінність даних**

У функціональному програмуванні, дані вважаються незмінними, тобто вони не можуть бути змінені після створення.

*Приклад:*
```python
def append_to_list(value, lst=[]):
    return lst + [value]

my_list = [1, 2, 3]
new_list = append_to_list(4, my_list)
```

У цьому прикладі, `my_list` залишається незмінним.

---

**3. Вищі функції**

Це функції, які приймають інші функції як аргументи або повертають функції.

*Приклад:*
```python
def apply(func, x, y):
    return func(x, y)

result = apply(add, 5, 3)  # Виведе: 8
```

---

**4. Каррінг та часткове застосування**

Каррінг — це техніка перетворення функції, яка приймає кілька аргументів, у послідовність функцій, кожна з яких приймає один аргумент.

*Приклад:*
```python
def multiply(x):
    def inner(y):
        return x * y
    return inner

double = multiply(2)
print(double(5))  # Виведе: 10
```

Часткове застосування — це техніка фіксації одного або декількох аргументів функції, створюючи нову функцію.

*Приклад за допомогою `functools.partial`:*
```python
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
print(square(5))  # Виведе: 25
```

---

**5. Рекурсія**

Рекурсія — це коли функція викликає сама себе.

*Приклад рекурсивної функції обчислення факторіалу:*
```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # Виведе: 120
```



**Основи функціонального програмування в Python**
---

**1. Визначення та створення функцій**

У Python функції визначаються за допомогою ключового слова `def`.

*Приклад стандартної функції:*
```python
def greet(name):
    return f"Вітаємо, {name}!"
```

---

**1.1 Приклади стандартних функцій**

```python
def add(a, b):
    return a + b

def is_even(num):
    return num % 2 == 0
```

---

**1.2 Локальні та глобальні змінні**

Змінні, визначені всередині функції, є локальними для цієї функції. Змінні, визначені поза функцією, є глобальними.

*Приклад:*
```python
global_variable = "Я глобальна змінна"

def demonstrate_variables():
    local_variable = "Я локальна змінна"
    print(global_variable)
    print(local_variable)

demonstrate_variables()
```

Зверніть увагу: Якщо ви хочете модифікувати глобальну змінну всередині функції, вам потрібно використовувати ключове слово `global`.

---

**2. Анонімні функції**

У Python анонімні функції визначаються за допомогою ключового слова `lambda`.

---

**2.1 `lambda`**

Форма `lambda` використовується для створення невеликих анонімних функцій. Ці функції можна використовувати в будь-якому місці, де потрібні об'єкти функцій.

*Приклад використання `lambda`:*
```python
multiply = lambda x, y: x * y
print(multiply(3, 4))  # Виведе: 12
```

---

**2.2 Приклади застосування `lambda` функцій**

`lambda` функції часто використовуються з функціями, які приймають функції як аргументи, такими як `map`, `filter` та `reduce`.

```python
numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x**2, numbers))
print(squared_numbers)  # Виведе: [1, 4, 9, 16, 25]
```

```python
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Виведе: [2, 4]
```



**Вбудовані функції Python**
---

Використання `map()`, `filter()` та `reduce()` може суттєво полегшити ваш код і зробити його більш читабельним. Ці функції дозволяють писати виразні операції обробки списків без необхідності використовувати цикли.

**1. `map()`: Приклади роботи з `map`**

Функція `map()` приймає функцію і список як аргументи. Вона повертає новий список, що містить результат застосування функції до кожного елемента списку.

*Приклад:*

```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
print(squared)  # Виведе: [1, 4, 9, 16, 25]
```

Також можна використовувати звичайні функції замість лямбда-функцій:
```python
def square(x):
    return x**2

squared = list(map(square, numbers))
print(squared)  # Виведе: [1, 4, 9, 16, 25]
```

---

**2. `filter()`: Фільтрація списку за допомогою `filter`**

Функція `filter()` використовується для фільтрації елементів списку. Вона повертає новий список, який містить тільки ті елементи, для яких функція повернула `True`.

*Приклад:*
```python
numbers = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # Виведе: [2, 4]
```

Також можна використовувати звичайні функції:
```python
def is_even(x):
    return x % 2 == 0

evens = list(filter(is_even, numbers))
print(evens)  # Виведе: [2, 4]
```

---

**3. `reduce()`: Агрегація даних з допомогою `reduce`**

Для використання `reduce()` спочатку потрібно імпортувати її з модуля `functools`. Функція `reduce()` застосовує функцію до елементів списку послідовно, агрегуючи результат. Вона повертає єдине значення.

*Приклад:*
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]
sum_of_numbers = reduce(lambda x, y: x + y, numbers)
print(sum_of_numbers)  # Виведе: 15
```

Тут `reduce()` послідовно застосовує функцію до елементів списку: ((1 + 2) + 3) + 4) + 5 = 15.



**Декоратори**
---

**1. Визначення та основи роботи з декораторами**

Декоратори — це, по суті, функції, які дозволяють модифікувати функціональність інших функцій або класів. Вони використовуються в Python для розширення функціоналу без зміни коду.

*Приклад:*
```python
def simple_decorator(func):
    def wrapper():
        print("Function started")
        func()
        print("Function ended")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello!")

say_hello()
```
Виведе:
```
Function started
Hello!
Function ended
```

---

**2. Створення власних декораторів**

a) **Приклади декораторів для вимірювання часу виконання**

Для вимірювання часу виконання функції можна використовувати декоратор:

```python
import time

def timer_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Function {func.__name__} took {end_time - start_time:.2f} seconds to run.")
        return result
    return wrapper

@timer_decorator
def example_function():
    time.sleep(2)
    print("Function executed")

example_function()
```
Виведе:
```
Function executed
Function example_function took 2.00 seconds to run.
```

b) **Декоратори з параметрами**

Декоратор може також приймати параметри:

```python
def repeat_decorator(num_times):
    def decorator_repeat(func):
        def wrapper(*args, **kwargs):
            for _ in range(num_times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator_repeat

@repeat_decorator(num_times=3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```
Виведе:
```
Hello, Alice!
Hello, Alice!
Hello, Alice!
```

Тут декоратор `repeat_decorator` приймає аргумент `num_times`, який вказує, скільки разів потрібно виконати функцію.

### **Додаткова інформація**

**Розуміння `*`, `**`, `*args`, та `**kwargs` в Python**

1. **`*` та `*args`:** 

Оператор `*` використовується для передачі невизначеної кількості позиційних аргументів у функцію. Це дозволяє функції приймати будь-яку кількість позиційних аргументів. У конвенції часто використовують термін `args`.

*Приклад:*
```python
def func(*args):
    for arg in args:
        print(arg)

func(1, 2, 3, 4)
```

2. **`**` та `**kwargs`:** 

Оператор `**` використовується для передачі невизначеної кількості іменованих (ключових) аргументів у функцію. Це дозволяє функції приймати будь-яку кількість ключових аргументів. У конвенції часто використовують термін `kwargs`, що означає "keyword arguments".

*Приклад:*
```python
def func(**kwargs):
    for key, value in kwargs.items():
        print(f"{key} = {value}")

func(a=1, b=2, c=3)
```

---

**Використання вкладених функцій у декораторах**

Вкладені функції це функції, що визначені всередині інших функцій. У контексті декораторів, вони надзвичайно корисні, оскільки дозволяють "обгортати" функцію, яку ми декоруємо.

Така структура є типовою для декораторів:

```python
def decorator(func):       # Зовнішня функція
    def wrapper():         # Вкладена (або обгорткова) функція
        # Додатковий код
        func()             # Виклик оригінальної функції
        # Додатковий код
    return wrapper
```

Вкладена функція `wrapper` "обгортає" функціональність декорованої функції, дозволяючи виконувати певний код до та/або після виклику оригінальної функції.



**Функціональні бібліотеки для Python**
---

1. **`functools`: корисні утиліти для підтримки функціонального стилю**

Модуль `functools` надає набір високорівневих функцій, які допомагають працювати з функціями та іншими викликаємими об'єктами.

- **`functools.partial`**: дозволяє зменшити кількість аргументів функції.

```python
from functools import partial

def multiply(x, y):
    return x * y

double = partial(multiply, 2)
print(double(4))  # Виведе: 8
```

- **`functools.lru_cache`**: декоратор, який додає кешування до функції.

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(10))  # Виведе: 55
```

- **`functools.reduce`**: виконує агрегуючу функцію на списку. В інших версіях Python ця функція була в глобальному просторі імен.

```python
from functools import reduce

result = reduce(lambda x, y: x*y, [1, 2, 3, 4, 5])
print(result)  # Виведе: 120
```

2. **`itertools`: ефективна робота з ітераторами**

Модуль `itertools` надає набір інструментів для створення та роботи з ітераторами.

- **`itertools.chain`**: об'єднує декілька ітераторів.

```python
import itertools

combined = itertools.chain([1, 2, 3], [4, 5, 6])
print(list(combined))  # Виведе: [1, 2, 3, 4, 5, 6]
```

- **`itertools.cycle`**: повертає елементи з ітерабельного об'єкта, повторюючи їх нескінченно.

```python
import itertools

counter = itertools.cycle([1, 2, 3])
print(next(counter))  # Виведе: 1
print(next(counter))  # Виведе: 2
print(next(counter))  # Виведе: 3
print(next(counter))  # Виведе: 1 (і так далі...)
```

- **`itertools.filterfalse`**: повертає елементи, для яких функція-предикат повертає `False`.

```python
import itertools

filtered = itertools.filterfalse(lambda x: x % 2==0, [1, 2, 3, 4, 5])
print(list(filtered))  # Виведе: [1, 3, 5]
```

