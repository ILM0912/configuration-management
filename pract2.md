# Практическая работа №2
## Задача 1
Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
### Код: 
```
pip show matplotlib
git clone https://github.com/matplotlib/matplotlib.git
```
![1](https://github.com/user-attachments/assets/3426c033-9f42-43cc-b347-dffded741ef9)
![1-2](https://github.com/user-attachments/assets/2bef146f-f153-4def-badf-e3217e540881)



## Задача 2
Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
### Код:
```
npm info express
git clone https://github.com/expressjs/express.git
```
![2-1](https://github.com/user-attachments/assets/39823d80-e2ca-4282-9dc4-9bc066a0361f)
![2-2](https://github.com/user-attachments/assets/ff8d9dbc-3863-4b54-896c-ed9f09fda9f9)



## Задача 3
Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.
### Код:
```
echo 'digraph G { node [shape=box]; matplotlib [label="matplotlib"]; numpy [label="numpy"]; pillow [label="pillow"]; cycler [label="cycler"]; matplotlib -> numpy; matplotlib -> pillow; matplotlib -> cycler; }' > matplotlib.dot
echo 'digraph G { node [shape=box]; express [label="express"]; accepts [label="accepts"]; array_flatten [label="array-flatten"]; content_type [label="content-type"]; express -> accepts; express -> array_flatten; express -> content_type; }' > express.dot
dot -Tpng matplotlib.dot -o matplotlib.png
dot -Tpng express.dot -o express.png
fim matplotlib.png
fim express.png
```
![3-1](https://github.com/user-attachments/assets/646f2729-390f-47d1-ad00-6186aedd4267)
![3-2](https://github.com/user-attachments/assets/86294142-4438-4d45-8265-5ee53cdd3f27)



## Задача 4
Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.
Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.
### Код:
```
include "globals.mzn";
array[1..6] of var 0..9: digits;
constraint all_different(digits);
constraint sum(digits[1..3]) = sum(digits[4..6]);
var int: min_sum = sum(digits[1..3]);
output ["Digits: ", show(digits), "\nSum of first three digits: ", show(min_sum)];
```
![4](https://github.com/user-attachments/assets/4d5e5cf8-0f54-41a0-8209-4d0650875a55)



## Задача 5
Решить на MiniZinc задачу о зависимостях пакетов для рисунка, приведенного ниже.
### Код:
```
enum PACKAGES = { root, menu_1_0_0, menu_1_1_0, menu_1_2_0, menu_1_3_0, menu_1_4_0, menu_1_5_0, dropdown_1_8_0, dropdown_2_0_0, dropdown_2_1_0, dropdown_2_2_0, dropdown_2_3_0, icons_1_0_0, icons_2_0_0 };

array[PACKAGES] of var 0..1: installed;
constraint installed[root] == 1;

constraint ((installed[root] == 1 -> installed[menu_1_0_0] == 1) \/ 
    (installed[root] == 1 -> installed[menu_1_1_0] == 1) \/
    (installed[root] == 1 -> installed[menu_1_2_0] == 1) \/
    (installed[root] == 1 -> installed[menu_1_3_0] == 1) \/
    (installed[root] == 1 -> installed[menu_1_4_0] == 1) \/
    (installed[root] == 1 -> installed[menu_1_5_0] == 1));
    
constraint (installed[root] == 1 -> installed[icons_1_0_0] == 1);

constraint (installed[menu_1_1_0] == 1 -> installed[dropdown_2_3_0] == 1) \/ 
    (installed[menu_1_1_0] == 1 -> installed[dropdown_2_2_0] == 1) \/ 
    (installed[menu_1_1_0] == 1 -> installed[dropdown_2_1_0] == 1) \/  
    (installed[menu_1_1_0] == 1 -> installed[dropdown_2_0_0] == 1);
constraint (installed[menu_1_2_0] == 1 -> installed[dropdown_2_3_0] == 1) \/ 
    (installed[menu_1_2_0] == 1 -> installed[dropdown_2_2_0] == 1) \/ 
    (installed[menu_1_2_0] == 1 -> installed[dropdown_2_1_0] == 1) \/  
    (installed[menu_1_2_0] == 1 -> installed[dropdown_2_0_0] == 1);
constraint (installed[menu_1_3_0] == 1 -> installed[dropdown_2_3_0] == 1) \/ 
    (installed[menu_1_3_0] == 1 -> installed[dropdown_2_2_0] == 1) \/ 
    (installed[menu_1_3_0] == 1 -> installed[dropdown_2_1_0] == 1) \/  
    (installed[menu_1_3_0] == 1 -> installed[dropdown_2_0_0] == 1);
constraint (installed[menu_1_4_0] == 1 -> installed[dropdown_2_3_0] == 1) \/ 
    (installed[menu_1_4_0] == 1 -> installed[dropdown_2_2_0] == 1) \/ 
    (installed[menu_1_4_0] == 1 -> installed[dropdown_2_1_0] == 1) \/  
    (installed[menu_1_4_0] == 1 -> installed[dropdown_2_0_0] == 1);
constraint (installed[menu_1_5_0] == 1 -> installed[dropdown_2_3_0] == 1) \/ 
    (installed[menu_1_5_0] == 1 -> installed[dropdown_2_2_0] == 1) \/ 
    (installed[menu_1_5_0] == 1 -> installed[dropdown_2_1_0] == 1) \/  
    (installed[menu_1_5_0] == 1 -> installed[dropdown_2_0_0] == 1);
    
constraint (installed[menu_1_0_0] == 1) -> (installed[dropdown_1_8_0] == 1);
constraint ((installed[dropdown_2_0_0] == 1) -> (installed[icons_2_0_0] == 1));
constraint ((installed[dropdown_2_1_0] == 1) -> (installed[icons_2_0_0] == 1));
constraint ((installed[dropdown_2_2_0] == 1) -> (installed[icons_2_0_0] == 1));
constraint ((installed[dropdown_2_3_0] == 1) -> (installed[icons_2_0_0] == 1));

solve minimize(sum(installed));
output ["Installed packages: ", show(installed)];
```
![5(new)](https://github.com/user-attachments/assets/25d31e65-27cb-44fa-b8fc-82442a6bfd33)


## Задача 6
Решить на MiniZinc задачу о зависимостях пакетов для следующих данных:
```
root 1.0.0 зависит от foo ^1.0.0 и target ^2.0.0.
foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0.
foo 1.0.0 не имеет зависимостей.
left 1.0.0 зависит от shared >=1.0.0.
right 1.0.0 зависит от shared <2.0.0.
shared 2.0.0 не имеет зависимостей.
shared 1.0.0 зависит от target ^1.0.0.
target 2.0.0 и 1.0.0 не имеют зависимостей.
```
### Код:
```
enum PACKAGES = {root, foo_1_0_0, foo_1_1_0, target_1_0_0, target_2_0_0, left_1_0_0, right_1_0_0, shared_1_0_0, shared_2_0_0};

array[PACKAGES] of var 0..1: installed;
constraint installed[root] == 1;

constraint ((installed[root] == 1 -> installed[foo_1_0_0] == 1) \/ 
    (installed[root] == 1 -> installed[foo_1_1_0] == 1));
    
constraint (installed[root] == 1 -> installed[target_2_0_0] == 1);

constraint ((installed[foo_1_1_0] == 1 -> installed[left_1_0_0] == 1) \/ 
    (installed[foo_1_1_0] == 1 -> installed[right_1_0_0] == 1));
    
constraint ((installed[left_1_0_0] == 1 -> installed[shared_1_0_0] == 1) \/ 
    (installed[left_1_0_0] == 1 -> installed[shared_2_0_0] == 1));
    
constraint (installed[right_1_0_0] == 1 -> installed[shared_1_0_0] == 1);

constraint (installed[shared_1_0_0] == 1 -> installed[target_1_0_0] == 1);

solve minimize(sum(installed));
output ["Installed packages: ", show(installed)];
```
![6](https://github.com/user-attachments/assets/4a4f6790-715a-488b-8f46-297410f49591)

## Задача 7
Представить задачу о зависимостях пакетов в общей форме. Здесь необходимо действовать аналогично реальному менеджеру пакетов. То есть получить описание пакета, а также его зависимости в виде структуры данных. Например, в виде словаря. В предыдущих задачах зависимости были явно заданы в системе ограничений. Теперь же систему ограничений надо построить автоматически, по метаданным.

### Код на python:
```python
packages = {
    "root": {"dependencies": ["^foo_1_0_0", "<=target_2_0_0"]},
    "foo_1_1_0": {"dependencies": ["^left_1_0_0", "^right_1_0_0"]},
    "left_1_0_0": {"dependencies": [">=shared_1_0_0"]},
    "right_1_0_0": {"dependencies": ["<shared_2_0_0"]},
    "shared_1_0_0": {"dependencies": ["^target_1_0_0"]},
    "shared_2_0_0": {"dependencies": []},
    "target_1_0_0": {"dependencies": []},
    "target_2_0_0": {"dependencies": []}
}
cnt_pack = {}
keys_list = list(packages.keys())
for key in keys_list:
    cnt_pack[key.split('_')[0]] = 'constraint ('
    
def satisfy_condition(condition):
    result = ""
    if condition.startswith('^'):
        base_version = condition[1:].split('_')
        for key in keys_list:
            check_vers = key.split('_')
            if key.startswith(base_version[0]) and check_vers[1] == base_version[1] and check_vers[1] >= base_version[2]:
                result += f"installed[{key}] == 1 \/ "
        result = result[:-4]
    elif condition.startswith('>='):
        base_version = condition[2:].split('_')
        for key in keys_list:
            check_vers = key.split('_')
            if key.startswith(base_version[0]) and (check_vers[1] > base_version[1] or (check_vers[1] == base_version[1] and check_vers[2] >= base_version[2])):
                result += f"installed[{key}] == 1 \/ "
        result = result[:-4]
    elif condition.startswith('<='):
        base_version = condition[2:].split('_')
        for key in keys_list:
            check_vers = key.split('_')
            if key.startswith(base_version[0]) and (check_vers[1] < base_version[1] or (check_vers[1] == base_version[1] and check_vers[2] <= base_version[2])):
                result += f"installed[{key}] == 1 \/ "
        result = result[:-4]
    elif condition.startswith('<'):
        base_version = condition[1:].split('_')
        for key in keys_list:
            check_vers = key.split('_')
            if key.startswith(base_version[0]) and (check_vers[1] < base_version[1] or (check_vers[1] == base_version[1] and
                                                                                         check_vers[2] < base_version[2])):
                result += f"installed[{key}] == 1 \/ "
        result = result[:-4]
    elif condition.startswith('>'):
        base_version = condition[1:].split('_')
        for key in keys_list:
            check_vers = key.split('_')
            if key.startswith(base_version[0]) and (check_vers[1] > base_version[1] or (check_vers[1] == base_version[1] and
                                                                                         check_vers[2] > base_version[2])):
                result += f"installed[{key}] == 1 \/ "
        result = result[:-4]
    return "(" + result + ")"

def generate_minizinc_code(packages):
    package_names = ', '.join(keys_list)
    minizinc_code = f"enum PACKAGES = {{{package_names}}};\n"
    minizinc_code += "array[PACKAGES] of var 0..1: installed;\n\n"
    minizinc_code += "constraint installed[root] == 1;\n"
    for package, details in packages.items():
        dependencies = details["dependencies"]
        if dependencies:
            dep_constraints = []
            for dep in dependencies:
                if dep.startswith(('^', '>=', '<=', '>', '<')):
                    constraint = satisfy_condition(dep)
                    if constraint:
                        dep_constraints.append(constraint)
                else:
                    dep_constraints.append(f"installed[{dep}] == 1")
            constraint = "constraint installed[{}] == 1 -> ({});\n".format(
                package, ' /\\ '.join(dep_constraints)
            )
            minizinc_code += constraint
    minizinc_code += "\n"
    for i in keys_list:
        cnt_pack[i.split('_')[0]] += f"installed[{i}] + "
    for i in list(cnt_pack.keys()):
        minizinc_code += cnt_pack[i][:-3] + ") <= 1;\n"
        
    minizinc_code += "\nsolve minimize sum(installed);\n"
    return minizinc_code

minizinc_code = generate_minizinc_code(packages)
print(minizinc_code)
```
### Сгенерированный код на MiniZinc:
```
enum PACKAGES = {root, foo_1_1_0, left_1_0_0, right_1_0_0, shared_1_0_0, shared_2_0_0, target_1_0_0, target_2_0_0};
array[PACKAGES] of var 0..1: installed;

constraint installed[root] == 1;
constraint installed[root] == 1 -> ((installed[foo_1_1_0] == 1) /\ (installed[target_1_0_0] == 1 \/ installed[target_2_0_0] == 1));
constraint installed[foo_1_1_0] == 1 -> ((installed[left_1_0_0] == 1) /\ (installed[right_1_0_0] == 1));
constraint installed[left_1_0_0] == 1 -> ((installed[shared_1_0_0] == 1 \/ installed[shared_2_0_0] == 1));
constraint installed[right_1_0_0] == 1 -> ((installed[shared_1_0_0] == 1));
constraint installed[shared_1_0_0] == 1 -> ((installed[target_1_0_0] == 1));

constraint (installed[root]) <= 1;
constraint (installed[foo_1_1_0]) <= 1;
constraint (installed[left_1_0_0]) <= 1;
constraint (installed[right_1_0_0]) <= 1;
constraint (installed[shared_1_0_0] + installed[shared_2_0_0]) <= 1;
constraint (installed[target_1_0_0] + installed[target_2_0_0]) <= 1;

solve minimize sum(installed);
```
![image](https://github.com/user-attachments/assets/d7e9f3c2-90cd-4122-b612-9cdf22fd8651)
![image](https://github.com/user-attachments/assets/63c9d798-7e3a-45b4-89c0-4d592066a15a)
в качестве примера используется следующие входные данные: 
```
root 1.0.0 зависит от foo ^1.0.0 и target <=2.0.0.
foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0.
left 1.0.0 зависит от shared >=1.0.0.
right 1.0.0 зависит от shared <2.0.0.
shared 2.0.0 не имеет зависимостей.
shared 1.0.0 зависит от target ^1.0.0.
target 2.0.0 и 1.0.0 не имеют зависимостей.
```
ответ: 
```
installed = [root: 1, foo_1_1_0: 1, left_1_0_0: 1, right_1_0_0: 1, shared_1_0_0: 1, shared_2_0_0: 0, target_1_0_0: 1, target_2_0_0: 0];
```
