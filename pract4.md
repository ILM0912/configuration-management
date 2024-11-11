# Практическое задание №4.

## Задача 1

На сайте https://onlywei.github.io/explain-git-with-d3 или http://git-school.github.io/visualizing-git/ (цвета могут отличаться, есть команды undo/redo) с помощью команд эмулятора git получить следующее состояние проекта (сливаем master с first, перебазируем second на master)

### Результат:
![image](https://github.com/user-attachments/assets/9725a211-8cef-4718-93d1-b20d2ee0aa66)

## Задача 2

Создать локальный git-репозиторий. Задать свои имя и почту (далее – coder1). Разместить файл prog.py с какими-нибудь данными. Прислать в текстовом виде диалог с git.
### Результат:
![image](https://github.com/user-attachments/assets/a6636246-9abe-4ae3-8a43-beeb3e1e2951)

## Задача 3

Создать рядом с локальным репозиторием bare-репозиторий с именем server. Загрузить туда содержимое локального репозитория. Команда git remote -v должна выдать информацию о server! Синхронизировать coder1 с server.
Клонировать репозиторий server в отдельной папке. Задать для работы с ним произвольные данные пользователя и почты (далее – coder2). Добавить файл readme.md с описанием программы. Обновить сервер.
Coder1 получает актуальные данные с сервера. Добавляет в readme в раздел об авторах свою информацию и обновляет сервер.
Coder2 добавляет в readme в раздел об авторах свою информацию и решает вопрос с конфликтами.
Прислать список набранных команд и содержимое git log.
### Результат:
![image](https://github.com/user-attachments/assets/f817a183-38c6-4421-bcd7-11725df86709)
![image](https://github.com/user-attachments/assets/0ce8e5fe-fd23-4fc8-a23c-885710964c41)
![image](https://github.com/user-attachments/assets/d255c48e-41ad-454d-8abb-71a5916933ff)
![image](https://github.com/user-attachments/assets/47743e4b-cfa7-4c74-ba45-1bebe4492ed7)


## Задача 4

Написать программу на Питоне (или другом ЯП), которая выводит список содержимого всех объектов репозитория. Воспользоваться командой "git cat-file -p". Идеальное решение – не использовать иных сторонних команд и библиотек для работы с git.
### Код: 
```python
import subprocess
import os
def get_git_objects(repo_path='.'):
    if not(os.path.isdir(os.path.join(repo_path, '.git'))):
        print("Это не гит репозиторий")
    for folder in os.listdir(os.path.join(repo_path, '.git', 'objects')):
        if folder in ['info', 'pack']:
            continue
        for file in os.listdir(os.path.join(repo_path, '.git', 'objects', folder)):
            hexsha = folder+file
            print(f"hexsha - {hexsha}\n")
            result = subprocess.run(
                ['git', 'cat-file', '-p', hexsha],
                cwd=repo_path,
                stdout=subprocess.PIPE,
                stderr=subprocess.PIPE)
            if result.returncode == 0:
                print(result.stdout.decode(errors='replace'))
            else:
                print(f"Ошибка при обработке объекта: {hexsha}\n{result.stderr}")
            print('\n' + '-' * 100 + '\n')
get_git_objects()
```
### Результат:
![image](https://github.com/user-attachments/assets/8a275d78-0211-471b-8a2f-1d512ce64ba5)

