# Домашня робота 2

**ПІБ:** Кручина Вадим  
**Файл для GitHub:** `/kruchyna_homework_2.md`

> Примітка до середовища: команди виконувались у **macOS (Darwin)**; використано еквіваленти шляхів і утиліт GNU/Linux (`/Users/...`, `dscl`, `id` замість типових у прикладах `/home/...` та записів у стилі `/etc/passwd`).

---

## Завдання 1. Ієрархія каталогів

### 1.1. Перейти в кореневий каталог `/` і показати вміст

Команди:

```bash
cd /
ls -la
```

Результат:

```text
total 11
drwxr-xr-x  22 root  wheel   704 22 лис 09:17 .
drwxr-xr-x  22 root  wheel   704 22 лис 09:17 ..
----------   1 root  admin     0 22 лис 09:17 .file
drwxr-xr-x   2 root  wheel    64 22 лис 09:17 .nofollow
drwxr-xr-x   2 root  wheel    64 22 лис 09:17 .resolve
drwxr-xr-x   2 root  wheel    64 22 лис 09:17 .vol
lrwxr-xr-x   1 root  admin    36 22 лис 09:17 .VolumeIcon.icns -> System/Volumes/Data/.VolumeIcon.icns
drwxrwxr-x  26 root  admin   832 28 кві 18:10 Applications
drwxr-xr-x@ 39 root  wheel  1248 22 лис 09:17 bin
drwxrwxr-t   2 root  admin    64  1 січ  2020 cores
dr-xr-xr-x   3 root  wheel  5254  1 січ  1970 dev
lrwxr-xr-x@  1 root  wheel    11 22 лис 09:17 etc -> private/etc
lrwxr-xr-x   1 root  wheel    25 20 бер 10:39 home -> /System/Volumes/Data/home
drwxr-xr-x  67 root  wheel  2144 18 січ 04:27 Library
drwxr-xr-x   2 root  wheel    64  1 січ  2020 opt
drwxr-xr-x   6 root  wheel   192  1 січ  1970 private
drwxr-xr-x@ 76 root  wheel  2432 22 лис 09:17 sbin
drwxr-xr-x@ 10 root  wheel   320 22 лис 09:17 System
lrwxr-xr-x@  1 root  wheel    11 22 лис 09:17 tmp -> private/tmp
drwxr-xr-x   6 root  admin   192 18 січ 04:26 Users
drwxr-xr-x@ 11 root  wheel   352 22 лис 09:17 usr
lrwxr-xr-x@  1 root  wheel    11 22 лис 09:17 var -> private/var
drwxr-xr-x   4 root  wheel   128  1 тра 16:58 Volumes
```

Пояснення: у корені відображаються системні каталоги та посилання (`bin`, `etc`, `usr`, `Users`, `private` тощо). На macOS структура відрізняється від типового Linux, але ідея «кореня файлової системи» та сама.

---

### 1.2. Перейти в `/etc` і показати вміст

Команди:

```bash
cd /etc
ls -la
```

Результат:

```text
total 848
drwxr-xr-x  80 root  wheel    2560 24 кві 14:08 .
drwxr-xr-x   6 root  wheel     192  1 січ  1970 ..
-rw-r--r--   1 root  wheel     515 22 лис 09:17 afpovertcp.cfg
lrwxr-xr-x   1 root  wheel      15 22 лис 09:17 aliases -> postfix/aliases
-rw-r-----   1 root  wheel   16384 22 лис 09:17 aliases.db
drwxr-xr-x   9 root  wheel     288 22 лис 09:17 apache2
drwxr-xr-x  16 root  wheel     512 22 лис 09:17 asl
-rw-r--r--   1 root  wheel    1051 22 лис 09:17 asl.conf
-rw-r--r--   1 root  wheel     149 22 лис 09:17 auto_home
-rw-r--r--   1 root  wheel     195 22 лис 09:17 auto_master
-rw-r--r--   1 root  wheel    1932 22 лис 09:17 autofs.conf
```

Пояснення: на macOS `/etc` зазвичай є символічним посиланням на `private/etc`; усередині лежать мережеві та системні конфігурації (`hosts`, `group` тощо).

---

### 1.3. Домашні каталоги користувачів (еквівалент «/home» на macOS)

На macOS домашні теки локальних користувачів зазвичай лежать у **`/Users`**, а не в `/home` (у корені часто є `home` як посилання, але перегляд `/home` нерідко дає `Operation not permitted` через політики доступу — це нормально для Mac).

```bash
cd /Users
pwd
ls -la
```

Результат:

```text
total 0
drwxr-xr-x    6 root   admin   192 18 січ 04:26 .
drwxr-xr-x   22 root   wheel   704 22 лис 09:17 ..
-rw-r--r--    1 root   wheel     0 22 лис 09:17 .localized
drwxr-xr-x+ 102 apple  staff  3264  2 тра 14:07 apple
drwxrwxrwt   28 root   wheel   896 18 січ 04:28 Shared
```

---

## Завдання 2. Файли, каталоги та посилання

Робочий каталог: `~/lab2_os_hw`. Повторне проходження: `rm -rf ~/lab2_os_hw`.

### 2.1. Створити новий каталог у домашньому каталозі

Команда:

```bash
mkdir -p ~/lab2_os_hw
```

Результат:

```text
```

---

### 2.2. Перейти в каталог і створити всередині файл

Команди:

```bash
cd ~/lab2_os_hw
echo 'Hello lab' > original.txt
ls -la original.txt
```

Результат:

```text
-rw-r--r--@ 2 apple  staff  10  2 тра 14:15 original.txt
```

---

### 2.3. Скопіювати файл у нове ім’я

Команди:

```bash
cp original.txt copy_original_name.txt
ls -la original.txt copy_original_name.txt
```

Результат:

```text
-rw-r--r--@ 1 apple  staff  10  2 тра 14:16 copy_original_name.txt
-rw-r--r--@ 2 apple  staff  10  2 тра 14:15 original.txt
```

---

### 2.4. Перейменувати копію

Команди:

```bash
mv copy_original_name.txt renamed.txt
ls -la original.txt copy_original_name.txt renamed.txt
```

Результат:

```text
ls: copy_original_name.txt: No such file or directory
-rw-r--r--@ 2 apple  staff  10  2 тра 14:15 original.txt
-rw-r--r--@ 1 apple  staff  10  2 тра 14:16 renamed.txt
```

---

### 2.5. Створити жорстке посилання

Команди:

```bash
ln original.txt link_to_original
ls -li original.txt hardlink_to_original
```

Результат:

```text
273495407 -rw-r--r--@ 3 apple  staff  10  2 тра 14:15 hardlink_to_original
273495407 -rw-r--r--@ 3 apple  staff  10  2 тра 14:15 original.txt
```

Пояснення: однаковий номер inode у колонці `ls -li` означає, що обидва імені вказують на один і той самий файл.

---

### 2.6. Створити символічне посилання

Команди:

```bash
ln -s renamed.txt symlink_to_renamed
ls -la symlink_to_renamed
```

Результат:

```text
lrwxr-xr-x@ 1 apple  staff  11  2 тра 14:20 symlink_to_renamed -> renamed.txt
```

---

### 2.7. Знайти файл за іменем

Створення тестового `file.txt` і пошук:

```bash
echo 'demo' > file.txt
find "$HOME/lab2_os_hw" -name 'file.txt'
```

Результат:

```text
/Users/apple/lab2_os_hw/file.txt
```

---

## Завдання 3. Права доступу

Файл для зміни прав: `~/lab2_os_hw/file.txt` (з завдання 2).

### 3.1. Переглянути права файлу

Команда:

```bash
ls -l file.txt
```

Результат:

```text
-rw-r--r--@ 1 apple  staff  5  2 тра 14:20 file.txt
```

---

### 3.2. Надати файлу права лише на читання (усі)

Команди:

```bash
chmod 444 ~/lab2_os_hw/file.txt
ls -l ~/lab2_os_hw/file.txt
```

Результат:

```text
-r--r--r--@ 1 apple  staff  5  2 тра 14:20 /Users/apple/lab2_os_hw/file.txt
```

---

### 3.3. Надати власнику право на запис

Команди:

```bash
chmod u+w file.txt
ls -l file.txt
```

Результат:

```text
-rw-r--r--@ 1 apple  staff  5  2 тра 14:20 file.txt
```

---

### 3.4. Переглянути значення `umask`

Команда:

```bash
umask
```

Результат:

```text
022
```

---

### 3.5. Встановити нове значення `umask`

Команди:

```bash
umask 023
umask
```

Результат:

```text
023
```

---

## Завдання 4. Користувачі (macOS)

### 4.1. Створити нового локального користувача `trainee`

Команда (пароль у прикладі замінюється на обраний при виконанні):

```bash
sudo sysadminctl -addUser trainee -fullName "Trainee" -password 'TemporaryPass123' -home /Users/trainee
```

Результат:

```text
2026-05-02 14:24:44.525 sysadminctl[42919:66173622] ----------------------------
2026-05-02 14:24:44.525 sysadminctl[42919:66173622] No clear text password or interactive option was specified (adduser, change/reset password will not allow user to use FDE) !
2026-05-02 14:24:44.525 sysadminctl[42919:66173622] ----------------------------
2026-05-02 14:24:45.258 sysadminctl[42919:66173622] Creating user record…
2026-05-02 14:24:46.388 sysadminctl[42919:66173622] Assigning UID: 503 GID: 20
2026-05-02 14:24:58.580 sysadminctl[42919:66173622] Home directory is assigned (not created!) at /Users/trainee
```

---

### 4.2. Додати користувача до групи адміністраторів macOS (`admin`, за функцією близько до групи `sudo` у Debian/Ubuntu)

Команда:

```bash
sudo dseditgroup -o edit -a trainee -t user admin
```

Результат:

```text
```

---

### 4.3. Перевірити, що користувач існує

Команда:

```bash
id trainee
```

Результат:

```text
uid=503(trainee) gid=20(staff) groups=20(staff),12(everyone),61(localaccounts),80(admin),701(com.apple.sharepoint.group.1),33(_appstore),98(_lpadmin),100(_lpoperator),204(_developer),250(_analyticsusers),395(com.apple.access_ftp),398(com.apple.access_screensharing),399(com.apple.access_ssh),400(com.apple.access_remote_ae)
```

---

## Висновок

Звіт фіксує виконання на macOS: перегляд `/`, `/etc`, каталогу `/Users`; операції з файлами та посиланнями; пошук `find`; зміну прав `chmod` і значення `umask`; створення користувача та призначення до групи `admin`.
