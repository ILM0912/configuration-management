# Задание 1: 
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

код:
```bash
grep -o '^[^:]*' /etc/passwd | sort
```
скрин:
![конфиг 1-1](https://github.com/user-attachments/assets/0c83d86b-4462-480d-9c48-354f407d571d)


# Задание 2: 
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

код:
```bash
grep -v '^#' /etc/protocols | tail -n 5 | sort -nrk2 | awk '{print $2, $1}'
```
скрин:
![конфиг 1-2](https://github.com/user-attachments/assets/0e3df6df-1993-4e96-a7cf-caf387ee14e9)


# Задание 3: 
Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

код:
```bash
#!/bin/bash

message="$1"
length=${#message}

echo -n "+"
for ((i=0;i<length+2;i++))
do
echo -n "-"
done
echo "+"

echo "| $message |"

echo -n "+"
for ((i=0;i<length+2;i++))
do
echo -n "-"
done
echo "+"
```
скрин:
![конфиг 1-3](https://github.com/user-attachments/assets/6c8dfab6-50d8-4304-b980-9d33db9666ad)


# Задание 4: 
Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

код:
```bash
grep -o '\b[a-zA-Z_][a-zA-Z0-9_]*\b' files_config/main1.c | sort | uniq
```

скрин:
![конфиг 1-4](https://github.com/user-attachments/assets/15e2a99b-ed49-476a-8588-0a7d0c153341)


# Задание 5: 
Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

код:
```bash
#!/bin/bash

chmod +x "$1"
sudo cp "$1" /usr/local/bin/
```

скрин:
![конфиг 1-5](https://github.com/user-attachments/assets/e8eadcf8-f6b6-466f-913b-f0bfa4e5e0e5)


# Задание 6: 
Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

код:
```bash
#!/bin/bash

for file in "$@"; do
  if [[ "$file" =~ \.(c|js|py)$ ]]; then
    first_line=$(head -n 1 "$file")
    if [[ "$first_line" =~ ^# && "$file" =~ \.(py)$ ]] || [[ "$first_line" =~ ^// && "$file" =~ \.(c|js)$ ]]; then
      echo "В файле $file есть комментарий в первой строке"
    else
      echo "В файле $file нет комментария в первой строке"
    fi
  fi
done
```

скрин:
![конфиг 1-6](https://github.com/user-attachments/assets/1cf06131-6e93-4976-9694-28c2419d97fd)


# Задание 7: 
Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

код:
```bash
#!/bin/bash

find "$1" -type f -exec md5sum {} + | sort | uniq -w32 -dD
```

скрин:
![конфиг 1-7](https://github.com/user-attachments/assets/01971fda-0e9f-4ce6-9a2e-8c16632944c3)


# Задание 8: 

