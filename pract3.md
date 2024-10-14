# Практическое занятие №3.

## Задача 1

Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.
### Код:
```
local createStudent(age, group, name) = {
  age: age,
  group: group,
  name: name,
};
local groups = [
      "ИКБО-" + (x) + "-23" for x in std.range(1, 24)
];
local students = [
  createStudent(19, 'ИКБО-4-20', 'Иванов И.И.'),
  createStudent(18, 'ИКБО-5-20', 'Петров П.П.'),
  createStudent(18, 'ИКБО-5-20', 'Сидоров С.С.'),
  createStudent(19, 'ИКБО-10-23', 'Красоткин А.А.'),
];
{
  groups: groups,
  students: students,
  subject: 'Конфигурационное управление',
}
```
![1](https://github.com/user-attachments/assets/68e1e18c-0687-4add-9616-6efe6546b228)

## Задача 2

Реализовать на Dhall приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.
### Код:
```
let List/map = https://prelude.dhall-lang.org/List/map
let List/generate = https://prelude.dhall-lang.org/v15.0.0/List/generate

let groups = List/generate 24 Text (\(n : Natural) -> "ИКБО-${Natural/show (n + 1)}-20")

let Student = { age : Natural, group : Text, name : Text }

let students : List Student = 
    [ { age = 19, group = "ИКБО-4-20", name = "Иванов И.И." }
    , { age = 18, group = "ИКБО-5-20", name = "Петров П.П." }
    , { age = 18, group = "ИКБО-5-20", name = "Сидоров С.С." }
    , { age = 19, group = "ИКБО-10-23", name = "Красоткин А.А." }
    ]

let subject : Text = "Конфигурационное управление"

in { groups = groups, students = students, subject = subject }
```
![2](https://github.com/user-attachments/assets/20310d10-cbaa-42de-aa8c-f80e20db089d)

## Задача 3

Язык нулей и единиц.

```
10
100
11
101101
000
```
### Код:
```
BNF = '''
E = 0 | 1 | 0 E | 1 E
'''
```
![3](https://github.com/user-attachments/assets/17ffd637-e29d-44fe-81fb-741351f4e310)

## Задача 4

Язык правильно расставленных скобок двух видов.
```
(({((()))}))
{}
{()}
()
{}
```
### Код:
```
BNF = '''
E = () | {} | ( E ) | { E } | E E 
'''
```
![4](https://github.com/user-attachments/assets/23586a70-d231-4dc7-9e8e-a2b9ea85c443)

## Задача 5

Язык выражений алгебры логики.

```
((~(y & x)) | (y) & ~x | ~x) & x
y & ~(y)
(~(y) & y & ~y)
~x
~((x) & y | (y) | (x)) & x | x | (y & ~y)
```
