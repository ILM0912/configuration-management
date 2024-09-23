### Задача 1
Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
# Код: 
pip show matplotlib
git clone https://github.com/matplotlib/matplotlib.git

![1](https://github.com/user-attachments/assets/3426c033-9f42-43cc-b347-dffded741ef9)
![1-2](https://github.com/user-attachments/assets/2bef146f-f153-4def-badf-e3217e540881)

### Задача 2
Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
# Код:
npm info express
git clone https://github.com/expressjs/express.git

![2-1](https://github.com/user-attachments/assets/39823d80-e2ca-4282-9dc4-9bc066a0361f)
![2-2](https://github.com/user-attachments/assets/ff8d9dbc-3863-4b54-896c-ed9f09fda9f9)



### Задача 3
Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.
# Код:
```bash
echo 'digraph G { node [shape=box]; matplotlib [label="matplotlib"]; numpy [label="numpy"]; pillow [label="pillow"]; cycler [label="cycler"]; matplotlib -> numpy; matplotlib -> pillow; matplotlib -> cycler; }' > matplotlib.dot
echo 'digraph G { node [shape=box]; express [label="express"]; accepts [label="accepts"]; array_flatten [label="array-flatten"]; content_type [label="content-type"]; express -> accepts; express -> array_flatten; express -> content_type; }' > express.dot
dot -Tpng matplotlib.dot -o matplotlib.png
dot -Tpng express.dot -o matplotlib.png
fim matplotlib.png
fim matplotlib.png```

![3-1](https://github.com/user-attachments/assets/646f2729-390f-47d1-ad00-6186aedd4267)
![3-2](https://github.com/user-attachments/assets/86294142-4438-4d45-8265-5ee53cdd3f27)



### Задача 4
Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.
Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.
# Код:
```MiniZinc
include "globals.mzn";
array[1..6] of var 0..9: digits;

constraint all_different(digits);

constraint sum(digits[1..3]) = sum(digits[4..6]);

var int: min_sum = sum(digits[1..3]);

output ["Digits: ", show(digits), "\nSum of first three digits: ", show(min_sum)];```
![4](https://github.com/user-attachments/assets/859dac6b-eaf4-4c04-908c-1665323c775a)
