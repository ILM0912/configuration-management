# Практическое задание №4.

## Задача 1

На сайте https://onlywei.github.io/explain-git-with-d3 или http://git-school.github.io/visualizing-git/ (цвета могут отличаться, есть команды undo/redo) с помощью команд эмулятора git получить следующее состояние проекта (сливаем master с first, перебазируем second на master)

### Результат:
![image](https://github.com/user-attachments/assets/9725a211-8cef-4718-93d1-b20d2ee0aa66)

## Задача 2

Создать локальный git-репозиторий. Задать свои имя и почту (далее – coder1). Разместить файл prog.py с какими-нибудь данными. Прислать в текстовом виде диалог с git.
### Результат:
![image](https://github.com/user-attachments/assets/4fb7dad4-7465-4757-9a0a-2fd01a3aac02)

## Задача 3

Создать рядом с локальным репозиторием bare-репозиторий с именем server. Загрузить туда содержимое локального репозитория. Команда git remote -v должна выдать информацию о server! Синхронизировать coder1 с server.
Клонировать репозиторий server в отдельной папке. Задать для работы с ним произвольные данные пользователя и почты (далее – coder2). Добавить файл readme.md с описанием программы. Обновить сервер.
Coder1 получает актуальные данные с сервера. Добавляет в readme в раздел об авторах свою информацию и обновляет сервер.
Coder2 добавляет в readme в раздел об авторах свою информацию и решает вопрос с конфликтами.
Прислать список набранных команд и содержимое git log.
### Результат:
![image](https://github.com/user-attachments/assets/3ec453be-784a-4a54-bbaf-c7ca1657c1c5)
![image](https://github.com/user-attachments/assets/6742930a-3108-4ebe-9cb6-7be7736cf5b3)
![image](https://github.com/user-attachments/assets/c2848009-9659-4bf6-b357-62c5f4c69e23)

## Задача 4

Написать программу на Питоне (или другом ЯП), которая выводит список содержимого всех объектов репозитория. Воспользоваться командой "git cat-file -p". Идеальное решение – не использовать иных сторонних команд и библиотек для работы с git.
### Код: 
```python
import subprocess

def get_git_objects(hexsha):
    result = subprocess.run(['git', 'cat-file', '-p', hexsha], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    result_type = subprocess.run(['git', 'cat-file', '-t', hexsha],stdout=subprocess.PIPE,stderr=subprocess.PIPE).stdout.decode()[:-1]
    if result.returncode == 0:
        for line in result.stdout.decode().splitlines():
            if line.startswith('parent') or line.startswith('tree'):
                next_hexsha = line.split()[1]
                get_git_objects(next_hexsha)
            if 'blob' in line:
                next_hexsha = line.split()[2]
                get_git_objects(next_hexsha)
        print(result_type + " - " + hexsha + '\n\n', result.stdout.decode(), "\n", "-"*50)
    else:
        print("Error:", result.stderr.decode())

get_git_objects("HEAD")
```
### Результат:
![image](https://github.com/user-attachments/assets/bfd8c688-35f6-461a-a4d1-04412aeb9778)
