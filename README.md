# Постановка задачи: индуктивно вычислять расстояние от выпуклой оболочки до заданного отрезка.
Для решения данной задачи был написан метод *min_dist*, который находит расстояние от точки до отрезка и расстояние между двумя отрезками.
В классе Polygon при вычислении расстояния до отрезка создается словарь adj_matrix, ключами которого являются ребра выпуклого многоугольника, а ключами - расстояния от них до заданного отрезка. Соответственно класс *Segmen*t был сделан хэшируемым.
Индуктивное вычисление расстояния заключается в следующем: находятся все затененные ребра и удаляются из словаря *adj_matrix*, а добавленные в результате метода add ребра добавляются в этот словарь, затем ищется минимум в словаре - это и есть искомое расстояние.

Пусть задана точка $M\in\mathbb{R}^2$ и отрезок, состоящий из точек $q, p \in\mathbb{R}^2$, обозначим $k = \frac{q.x - p.x}{q.y - p.y} $.

Тогда уравнение прямой проходящей через точки выглядит следующим образом: $y = kx + p.y - kp.x$

Уравнение проходящей через точку $M$ прямой, перпендикулярной данной: $y = M.y - \frac{1}{k}(x - M.x)$

![image](https://user-images.githubusercontent.com/110375755/190968323-a510fc97-2a09-451e-b314-eb2808d6ed3a.png)

### Постановка задачи

Необходимо написать программу, находящую выпуклую оболочку последовательно
поступающих точек плоскости и вычисляющую её периметр и площадь. Решение
должно быть индуктивным, что означает определение выпуклой оболочки и
вычисление её характеристик сразу после поступления очередной точки с
использованием методов теории индуктивных функций.

### Краткий комментарий к решению

- Ключевое понятие проекта: *освещённость ребра из точки* 
- Вспомогательные классы:
    - `R2Point` — точка на плоскости
    - `Deq` — контейнер дек (double ended queue)
- Основные классы:
    - `Figure` — «абстрактная» фигура
    - `Void` — нульугольник
    - `Point` — одноугольник
    - `Segment` — двуугольник
    - `Polygon` — многоугольник
- Файлы проекта:
    - `README.md` — данный файл
    - `README.html` — полученный из файла `README.md` `html`-файл
    - `r2point.py` — реализация класса `R2Point`
    - `deq.py` —  реализация класса `Deq`
    - `convex.py` — реализация основных классов
    - `run_convex.py` — файл запуска
    - `tk_drawer.py` — интерфейс к графической библиотеке
    - `run_tk_convex.py` — файл запуска с использованием графики
    - `tests/test_r2point.py` — тесты к классу `R2Point`
    - `tests/test_convex.py` — тесты к основным классам

Файлы `run_tk_convex.py` и `run_tk_convex.py` являются исполняемыми (они имеют
бит `x`), в первой строке каждого из них используется [шебанг](https://ru.wikipedia.org/wiki/%D0%A8%D0%B5%D0%B1%D0%B0%D0%BD%D0%B3_(Unix)) и команда `env` с
опцией (ключом) `-S`. Это обеспечивает передачу интерпретатору языка Python
опции (ключа) `-B`, отменяющего генерацию `pyc`-файлов в директории
`__pycache__`.

### Соблюдение соглашений о стиле программного кода

Для языка Python существуют [соглашения о стиле
кода](https://www.python.org/dev/peps/pep-0008/). Они являются лишь
рекомендациями (интерпретатор игнорирует их нарушение), но основную их
часть при написании программ целесообразно соблюдать. Существует простой
способ проверить соблюдение считающегося правильным
стиля записи кода с помощью утилиты (программы) `pycodestyle`. Утилита
`yapf` позволяет даже изменить код в соответствии с этими соглашениями.

Команда 

    pycodestyle r2point.py

позволяет, например, проверить соблюдение стиля для файла `r2point.py`.
С помощью очень мощной и часто используемой утилиты `find` проверить
корректность стиля всех файлов проекта можно так:

    find . -name '*.py' -exec pycodestyle {} \;

Эта команда находит все файлы с расширением `py` и запускает программу
`pycodestyle` последовательно для каждого из них.

### Запуск тестов

Уже известная нам команда (см. материал, посвящённый тестированию программ)

    python -B -m pytest -p no:cacheprovider tests

запускает pytest, выполняя все начинающиеся с `test` методы классов,
имена которых начинаются с `Test`, содержащиеся во всех файлах `test_*.py`
директории `tests`.

### Запуск программы

`./run_convex.py`

### Запуск программы с графическим интерфейсом

`./run_tk_convex.py`
