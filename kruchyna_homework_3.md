# Домашня робота 3

**ПІБ:** Кручина Вадим  
**Файл для GitHub:** `/kruchyna_homework_3.md`

> Примітка до середовища: команди орієнтовані на **macOS** (BSD `ps`, `top`). На GNU/Linux синтаксис `ps`/`top` може відрізнятис.

---

## Завдання 1. Огляд активних процесів

### 1.1. Список усіх процесів за допомогою `ps`

Команди (типовий варіант на macOS):

```bash
ps aux | head -5
```

Результат:

```text
USER               PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
_windowserver     7659  31,5  0,5 38932732  85728   ??  Ss   24кві26 1747:37.79 /System/Library/PrivateFrameworks/SkyLight.framework/Resources/WindowServer -daemon
apple             8421  11,4  0,1 33775840  16916   ??  S    24кві26 1513:34.12 /System/Library/CoreServices/ReportCrash agent
apple             9095   8,6  0,1 67694504  15948   ??  S    24кві26 792:25.95 /Applications/Postman.app/Contents/Frameworks/Postman Helper (GPU).app/Contents/MacOS/Postman Helper (GPU) --type=gpu-process --user-data-dir=/Users/apple/Library/Application Support/Postman --gpu-preferences=UAAAAAAAAAAgAAAEAAAAAAAAAAAAAAAAAABgAAEAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAEAAAAAAAAAAIAAAAAAAAAAgAAAAAAAAA --shared-files --field-trial-handle=1718379636,r,12030152458032959092,4225584097566069322,262144 --enable-features=ScreenCaptureKitPickerScreen,ScreenCaptureKitStreamPickerSonoma --disable-features=MacWebContentsOcclusion,SpareRendererForSitePerProcess,TimeoutHangingVideoCaptureStarts --variations-seed-version --seatbelt-client=34
apple             7738   7,7  0,4 35400036  73904   ??  S    24кві26   9:19.37 /System/Applications/Utilities/Terminal.app/Contents/MacOS/Terminal
```

Пояснення: `ps aux` виводить процеси всіх користувачів з розширеними полями (користувач, PID, CPU, MEM, VSZ, RSS, TTY, STAT, час запуску, команда).

---

### 1.2. Інтерактивний монітор `top`; процес із найбільшим споживанням RAM

Інтерактивний монітор:

```bash
top
```

---

### 1.3. PID поточної оболонки (bash/zsh)

Команда:

```bash
echo $$
```

Результат:

```text
87220
```

---

## Завдання 2. Робота у фоні та керування процесами

### 2.1. Довга команда у фоновому режимі

Команди:

```bash
sleep 1000 &
echo "Background PID: $!"
```

Результат:

```text
[1] 71494
Background PID: $
```

---

### 2.2. Список фонових завдань поточної оболонки

Команда:

```bash
jobs -l
```

Результат:

```text
[1]  - 71494 running    sleep 1000
```

---

### 2.3. Повернення процесу з фону на передній план

```bash
fg %1
```

```text
[1]  - 71494 running    sleep 1000
```

---

### 2.4. Зупинка процесу та примусове завершення через `kill`

```bash
kill 72076
```

Результат:

```text
72076 terminated  sleep 1000   
```

---

### 2.5. Команда через `nohup` (продовження після закриття терміналу)

Приклад:

```bash
nohup sleep 2000 > /tmp/nohup_sleep.log 2>&1
```

Результат:

```text
[1] 79918
```

Пояснення: `nohup` ігнорує SIGHUP при від’єднанні терміналу; вивід за замовчуванням ішов би в `nohup.out` у поточному каталозі — тут перенаправлено в `/tmp/nohup_sleep.log`.

---

## Завдання 3. Пріоритети та обмеження

### 3.1. Запуск команди з нижчим пріоритетом (більше `nice`)

Приклад (на macOS діапазон nice зазвичай від -20 до 20 для звичайного користувача; «повільніше» — **більше** число `nice`):

```bash
nice -n 15 sleep 60 &
jobs -l
```

Результат:

```text
[1] 90411
[1]  + 90411 running    nice -n 15 sleep 60
```

Пояснення: більше значення **nice** означає **нижчий** пріоритет планування CPU.

---

### 3.2. Зміна пріоритету вже запущеного процесу

Запустити допоміжний процес і запам’ятати PID:

```bash
sleep 300 &
SPID=$!
echo $SPID
```

Змінити nice для цього PID (на macOS часто потрібні права для сильного «покращення» пріоритету; зниження — зазвичай дозволено):

```bash
renice -n 10 -p $SPID
ps -p $SPID -o pid,nice,comm=
```

Результат:

```text
93282 15 sleep
```

Пояснення: `renice` змінює лічильник nice для живого процесу.

---

### 3.3. Поточні обмеження ресурсів (`ulimit`)

Команда:

```bash
ulimit -a
```

Результат:

```text
-t: cpu time (seconds)              unlimited
-f: file size (blocks)              unlimited
-d: data seg size (kbytes)          unlimited
-s: stack size (kbytes)             8192
-c: core file size (blocks)         0
-v: address space (kbytes)          unlimited
-l: locked-in-memory size (kbytes)  unlimited
-u: processes                       2784
-n: file descriptors                1048575
```

---

## Завдання 4. Моніторинг ресурсів

### 4.1. Використання дискового простору

Команда:

```bash
df -h
```

Результат:

```text
Filesystem        Size    Used   Avail Capacity iused ifree %iused  Mounted on
/dev/disk1s5s1   466Gi    11Gi   169Gi     7%    427k  1,8G    0%   /
devfs            221Ki   221Ki     0Bi   100%     766     0  100%   /dev
/dev/disk1s2     466Gi   4,3Gi   169Gi     3%    3,8k  1,8G    0%   /System/Volumes/Preboot
/dev/disk1s4     466Gi    19Gi   169Gi    11%      19  1,8G    0%   /System/Volumes/VM
/dev/disk1s6     466Gi    67Mi   169Gi     1%     597  1,8G    0%   /System/Volumes/Update
/dev/disk1s1     466Gi   260Gi   169Gi    61%    5,4M  1,8G    0%   /System/Volumes/Data
map auto_home      0Bi     0Bi     0Bi   100%       0     0     -   /System/Volumes/Data/home
/dev/disk1s5     466Gi    11Gi   169Gi     7%    427k  1,8G    0%   /System/Volumes/Update/mnt1
/dev/disk2s2      78Mi    38Mi    40Mi    49%     321  4,3G    0%   /Volumes/uTorrent Web
/dev/disk4s1     8,2Gi   8,0Gi   245Mi    98%      13  2,5M    0%   /Library/Developer/CoreSimulator/Cryptex/Images/bundle/SimRuntimeBundle-B2313D8C-F25C-4038-8BF1-CBAB0A000C0B
/dev/disk6s1      18Gi    18Gi   467Mi    98%    452k  4,8M    9%   /Library/Developer/CoreSimulator/Volumes/iOS_22B81
/dev/disk8s1     8,4Gi   8,1Gi   248Mi    98%      13  2,5M    0%   /Library/Developer/CoreSimulator/Cryptex/Images/bundle/SimRuntimeBundle-030FE95E-D2B1-415E-B9B2-96172F3B93FF
/dev/disk10s1     18Gi    18Gi   472Mi    98%    459k  4,8M    9%   /Library/Developer/CoreSimulator/Volumes/iOS_22C150
```

Пояснення: `df -h` показує змонтовані файлові системи з розмірами у зручних одиницях (K/M/G).

---

### 4.2. Вільна та використана оперативна пам’ять (зручний формат)

На macOS зручний однорядковий знімок:

```bash
top -l 1 -s 0 | grep PhysMem
```

Результат:

```text
PhysMem: 14G used (4432M wired, 1618M compressor), 1806M unused.
```

Пояснення: рядок **PhysMem** у виводі `top -l 1` містить узагальнення використаної/доступної RAM у МБ/ГБ. `vm_stat` використовує сторінки пам’яті (розмір сторінки: `pagesize` / `getconf PAGESIZE`).

---

## Висновок

У звіті зафіксовано роботу з `ps`, інтерактивним та одноразовим `top`, PID оболонки; фонові завдання (`&`, `jobs`, `fg`), сигнали `kill`, `nohup`; `nice` / `renice`, `ulimit -a`; `df -h` та перегляд RAM на macOS.
