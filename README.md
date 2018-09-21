# tp_lab_3
Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab03** и с лиценцией **MIT**
- [ ] 2. Ознакомиться со ссылками учебного материала
- [ ] 3. Выполнить инструкцию учебного материала
- [ ] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя> // Переменная и именем пользователя
$ export GITHUB_EMAIL=<адрес_почтового_ящика> // Переменная почтой
$ alias edit=<nano|vi|vim|subl> // Редактор по умолчания
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace // В папку
```

```ShellSession
$ mkdir projects/lab03 && cd projects/lab03 // Создаём папку для 3-ей лабы
$ git init // Создаём локальный репозиторий
$ git config --global user.name ${GITHUB_USERNAME} // Настраиваем глобальные параметры
$ git config --global user.email ${GITHUB_EMAIL}
$ git config -e --global // Просмотр настроек
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
$ git pull origin master // Пулим репозиторий /* remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/Elegiacal/lab03
* branch            master     -> FETCH_HEAD
* [new branch]      master     -> origin/master */

$ touch README.md // Создаём README.md
$ git status // Смотрим на состояние файлов /* On branch master
Untracked files:
(use "git add <file>..." to include in what will be committed)

README.md */

$ git add README.md // README.md staged
$ git commit -m"added README.md" // Готовим к отправке /* [master 23f3e99] Added README.md
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 README.md */

$ git push origin master // Заливаем /* Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 280 bytes | 280.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/elpidifor/lab03.git
8380524..23f3e99  master -> master */
```

Добавить на сервисе **GitHub** в репозитории **lab03** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master // Снова пулим репозиторий
$ git log // История коммитов /* commit db823814f103d3f4d136dc6d4f9a2ae171fba67a (HEAD -> master, origin/master)
Author: elpidifor <elpidifor011@yandex.ru>
Date:   Thu September 18 11:17:41 2018 +0300

Added .gitignore

commit 23f3e99d08b094fc5399f67e70b97b15ff8e62f8
Author: elpidifor <elpidifor011@yandex.ru>
Date:   Thu September 18 11:15:21 2018 +0300

Added README.md

commit 8380524f396df81f6d8fa5f033a69ffaac80ed28
Author: elpidifor <elpidifor011@yandex.ru>
Date:   Thu September 18 11:12:07 2018 +0300

Initial commit */
```

```ShellSession
$ mkdir sources // Создаём нужные подпапки
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF // Создаём нужные cpp/hpp файлы в соответствующих подпапках
#include <print.hpp>

void print(const std::string& text, std::ostream& out) {
  out << text;
}

void print(const std::string& text, std::ofstream& out) {
  out << text;
}
EOF
```

```ShellSession
$ cat > include/print.hpp <<EOF
#include <string>
#include <fstream>
#include <iostream>

void print(const std::string& text, std::ostream& out = std::cout);
void print(const std::string& text, std::ofstream& out);
EOF
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv) {
  print("hello");
}
EOF
```

```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <fstream>
#include <print.hpp>

int main(int argc, char** argv) {
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
$ edit README.md // Редактируем README.md
```

```ShellSession
$ git status // Статус
$ git add . // Все новые файлы – staged
$ git commit -m"added sources" // Коммитим
$ git push origin master // Пушим
```

## Report

```ShellSession
$ cd ~/workspace/labs/ // Создаём отчёт аналогично предыдущим лабам
$ export LAB_NUMBER=03 // Переменная с номером
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER} // Клонируем
$ mkdir reports/lab${LAB_NUMBER} //Новая папка для нового отчёта
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md // Копируем файл
$ cd reports/lab${LAB_NUMBER} // В папку
$ edit REPORT.md // Редактируем
$ gistup -m "lab${LAB_NUMBER}" // Заливаем на Gist
