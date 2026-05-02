# Домашня робота 1

**ПІБ:** Кручина Вадим  
**Файл для GitHub:** `/kruchyna_homework_1.md`

> Примітка до середовища виконання: команди виконувались у Linux-терміналі контейнера. Каталогу `Downloads` спочатку не було, тому його було створено для виконання завдання. Команда `man` у цьому контейнері не встановлена, тому для команд `man ls`, `man cat`, `man man` зафіксовано фактичний результат `command not found`. Відповіді на питання наведені за стандартною поведінкою GNU/Linux.

---

## Завдання 1. Базові команди

### 1.1. Покажи вміст домашнього каталогу

Команда:

```bash
pwd
ls -la
```

Результат:

```text
/Users/apple

total 3120
drwxr-xr-x+ 101 apple  staff    3232  2 тра 12:59 .
drwxr-xr-x    6 root   admin     192 18 січ 04:26 ..
drwxr-xr-x@   7 apple  staff     224 26 сер  2025 .android
drwxr-xr-x    7 apple  staff     224 25 бер  2022 .asdf
-rw-r--r--    1 apple  staff   35852  8 січ  2024 .babel.json
-rw-------@   1 apple  staff    6052 18 сер  2025 .bash_history
-rw-r--r--    1 apple  staff     622  3 бер 09:18 .bash_profile
drwx------   15 apple  staff     480 19 жов  2021 .bash_sessions
```

Пояснення: `pwd` показує поточний шлях, `ls -la` показує повний список файлів і каталогів, включно з прихованими файлами, які починаються з крапки.

---

### 1.2. Перейди у каталог Downloads і покажи його вміст

Команди:

```bash
cd /Downloads
pwd
ls -la
```

Результат:

```text
/Users/apple/Downloads

total 31348184
drwx------@ 201 apple  staff        6432  2 тра 11:34 .
drwxr-xr-x+ 101 apple  staff        3232  2 тра 12:54 ..
-rw-r--r--@   1 apple  staff       14340 16 кві 14:28 .DS_Store
-rw-r--r--    1 apple  staff           0 15 жов  2021 .localized
-rw-r--r--@   1 apple  staff      114257 28 кві 17:43 (uakino.me)_hobbt-pustka-smoa-gobt-pustka-smoa.torrent
-rw-------@   1 apple  staff       65137 30 жов  2025 1.jpg
-rw-------@   1 apple  staff      159598 29 жов  2025 100-Phrases.pdf
-rw-------@   1 apple  staff   121823156  8 лют 20:51 1631530151982.mp4
-rw-r--r--@   1 apple  staff     6614120 28 січ 15:01 16B5AFAEF224BA6A4E54F819DF516148.png
-rw-r--r--@   1 apple  staff      187846  8 бер 14:14 1772200179-8309.webp
-rw-------@   1 apple  staff    45235304 15 січ 12:40 2_5424685875445403048.mp4
-rw-------@   1 apple  staff      619656 24 жов  2025 2_5467843416232593176.pdf
```

Пояснення: `cd` змінює поточний каталог.

---

### 1.3. Створи порожній файл без `touch`

Команда:

```bash
: > empty_file.txt
```

Результат:

```text
```

Пояснення: `:` — це вбудована команда оболонки, яка нічого не робить, а перенаправлення `>` створює порожній файл або очищає файл, якщо він уже існує. Команда `touch` не використовувалась.

---

### 1.4. Переглянь вміст файлу

Команда:

```bash
cat empty_file.txt
```

Результат:

```text

```

Пояснення: вивід порожній, тому що файл `empty_file.txt` порожній.

---

### 1.5. Перейди у домашній каталог абсолютним шляхом

Команди:

```bash
cd
pwd
```

Результат:

```text
/Users/apple
```

---

### 1.6. Перейди у домашній каталог відносним шляхом

Команди:

```bash
cd Downloads
cd ..
pwd
```

Результат:

```text
/Users/apple
```

Пояснення: команда `cd ..` переходить на один рівень вище від поточного каталогу.

---

## Завдання 2. Робота з документацією

### 2.1. Виконання команди `man ls`

Команда:

```bash
man ls
```

Фактичний результат у контейнері:

```text
NAME
     ls – list directory contents

SYNOPSIS
     ls [-@ABCFGHILOPRSTUWabcdefghiklmnopqrstuvwxy1%,] [--color=when] [-D format] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls displays its name as well as any requested, associated information.  For each operand that names a file of type directory, ls
     displays the names of files contained within that directory, as well as any requested, associated information.

     If no operands are given, the contents of the current directory are displayed.  If more than one operand is given, non-directory operands are displayed first; directory and non-directory operands
     are sorted separately and in lexicographical order.
```

Пояснення: `man ls` відкриває сторінку документації для команди `ls`.

---

### 2.2. Виконання команди `help cd`

Команда:

```bash
bash -c "help cd"
```

Результат, початок виводу:

```text
cd: cd [-L|-P] [dir]
    Change the current directory to DIR.  The variable $HOME is the
    default DIR.  The variable CDPATH defines the search path for
    the directory containing DIR.  Alternative directory names in CDPATH
    are separated by a colon (:).  A null directory name is the same as
    the current directory, i.e. `.'.  If DIR begins with a slash (/),
    then CDPATH is not used.  If the directory is not found, and the
    shell option `cdable_vars' is set, then try the word as a variable
    name.  If that variable has a value, then cd to the value of that
    variable.  The -P option says to use the physical directory structure
    instead of following symbolic links; the -L option forces symbolic links
    to be followed.
```

Пояснення: `cd` є вбудованою командою оболонки Bash, тому довідку для неї можна переглянути через `help cd`.

---

### 2.3. Виконання команди `man cat`

Команда:

```bash
man cat
```

Фактичний результат у контейнері:

```text
NAME
     cat – concatenate and print files

SYNOPSIS
     cat [-belnstuv] [file ...]

DESCRIPTION
     The cat utility reads files sequentially, writing them to the standard output.  The file operands are processed in command-line order.  If file is a single dash (‘-’) or absent, cat reads from the
     standard input.  If file is a UNIX domain socket, cat connects to it and then reads it until EOF.  This complements the UNIX domain binding capability available in inetd(8).
```

Пояснення: `man cat` відкриває сторінку документації для команди `cat`.

---

### 2.4. Виконання команди `man man`

Команда:

```bash
man man
```

Фактичний результат у контейнері:

```text
NAME
     man, apropos, whatis – display online manual documentation pages

SYNOPSIS
     man [-adho] [-t | -w] [-M manpath] [-P pager] [-S mansect] [-m arch[:machine]] [-p [eprtv]] [mansect] page ...

     man -f [-d] [-M manpath] [-P pager] [-S mansect] keyword ...
     whatis [-d] [-s mansect] keyword ...

     man -k [-d] [-M manpath] [-P pager] [-S mansect] keyword ...
     apropos [-d] [-s mansect] keyword ...

DESCRIPTION
     The man utility finds and displays online manual documentation pages.  If mansect is provided, man restricts the search to the specific section of the manual.
```

Пояснення: `man man` відкриває документацію про саму систему manual pages.

---

### 2.5. Виконання команди `cp --help`

Команда:

```bash
cp --help
```

Результат, початок виводу:

```text
cp: illegal option -- -
usage: cp [-R [-H | -L | -P]] [-fi | -n] [-aclpSsvXx] source_file target_file
       cp [-R [-H | -L | -P]] [-fi | -n] [-aclpSsvXx] source_file ... target_directory
```

Пояснення: команда `cp --help` показує коротку довідку про копіювання файлів і каталогів.

---

### 2.6. Виконання команди `mv --help`

Команда:

```bash
mv --help
```

Результат, початок виводу:

```text
mv: illegal option -- -
usage: mv [-f | -i | -n] [-hv] source target
       mv [-f | -i | -n] [-v] source ... directory
```

Пояснення: команда `mv --help` показує коротку довідку про переміщення та перейменування файлів і каталогів.

---

### 2.7. Відповіді на питання

#### Який ключ `ls` показує приховані файли?

Ключ:

```bash
-a
```

Також можна використати довгу форму:

```bash
--all
```

Перевірка через `ls --help`:

```text
-a, --all                  do not ignore entries starting with .
-A, --almost-all           do not list implied . and ..
```

Відповідь: приховані файли показує ключ `-a` або `--all`. Ключ `-A` теж показує приховані файли, але не показує спеціальні записи `.` і `..`.

---

#### Який ключ у `cat` нумерує рядки?

Ключ:

```bash
-n
```

Також можна використати довгу форму:

```bash
--number
```

Перевірка через `cat --help`:

```text
-b, --number-nonblank    number nonempty output lines, overrides -n
-n, --number             number all output lines
```

Відповідь: усі рядки нумерує ключ `-n` або `--number`. Ключ `-b` нумерує тільки непорожні рядки.

---

#### Чим відрізняються `man` і `--help`?

`man` відкриває повну сторінку документації для команди. Зазвичай там є опис, синтаксис, список опцій, приклади, додаткова інформація та пов'язані команди.

`--help` показує коротку довідку прямо в терміналі. Зазвичай це швидкий список основних параметрів команди без такого детального пояснення, як у `man`.

Додатково: `help` без двох дефісів використовується в Bash для вбудованих команд оболонки, наприклад `help cd`, бо `cd` — це не окрема зовнішня програма, а команда самої оболонки.

---

## Завдання 3. Міні-сценарій

### Сценарій із 8 команд

Мета сценарію: перейти в каталог, створити файл, переглянути список файлів, перейти в інше місце, повернутись назад і переглянути документацію однієї з команд.

---

### 3.1. Створити каталог для сценарію

Команда:

```bash
mkdir scenario_demo
```

Результат:

```text
```

Пояснення: `mkdir` створює каталог, а якщо він уже існує — завершується помилкою.

---

### 3.2. Перейти в каталог

Команда:

```bash
cd scenario_demo
pwd
```

Результат:

```text
/Users/apple/neoversity/scenario_demo
```

Пояснення: команда `cd` переходить у каталог `scenario_demo`, а `pwd` підтверджує поточне місце.

---

### 3.3. Створити там один файл

Команда:

```bash
: > scenario_file.txt
```

Результат:

```text
```

Пояснення: файл `scenario_file.txt` створено без використання команди `touch`.

---

### 3.4. Переглянути список файлів

Команда:

```bash
ls -la
```

Результат:

```text
total 0
drwxr-xr-x   3 apple  staff   96  2 тра 13:14 .
drwxr-xr-x  11 apple  staff  352  2 тра 13:13 ..
-rw-r--r--   1 apple  staff    0  2 тра 13:14 scenario_file.txt
```

Пояснення: у списку видно створений файл `scenario_file.txt`.

---

### 3.5. Перейти в інше місце

Команда:

```bash
cd
pwd
```

Результат:

```text
/Users/apple
```

---

### 3.6. Повернутись назад

Команда:

```bash
cd -
```

Результат:

```text
~/neoversity/scenario_demo
```

Пояснення: команда `cd -` повертає до попереднього каталогу.

---

### 3.7. Перевірити поточний каталог

Команда:

```bash
pwd
```

Результат:

```text
/neoversity/scenario_demo
```

---

### 3.8. Переглянути документацію однієї з команд

Команда:

```bash
cp --help | head -5
```

Результат:

```text
cp: illegal option -- -
usage: cp [-R [-H | -L | -P]] [-fi | -n] [-aclpSsvXx] source_file target_file
       cp [-R [-H | -L | -P]] [-fi | -n] [-aclpSsvXx] source_file ... target_directory
```

Пояснення: команда `cp --help` показує довідку про команду `cp`, а `head -5` обмежує вивід першими п'ятьма рядками.

---

## Висновок

У роботі були виконані базові команди Linux для навігації файловою системою, перегляду вмісту каталогів, створення порожніх файлів без `touch`, перегляду файлів через `cat`, а також роботи з короткою документацією команд через `help` і `--help`. Також складено міні-сценарій із послідовністю команд для практичного закріплення навігації та роботи з файлами.
