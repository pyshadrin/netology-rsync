# Домашнее задание к занятию "`Резервное копирование`" - `Шадрин Петр`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания! 
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`rsync -av --delete --checksum --exclude='.*' ~/ /tmp/backup/`

<img width="655" height="678" alt="image" src="https://github.com/user-attachments/assets/cc48afe5-e1f4-4939-862b-7fc9006a2fa8" />


---

### Задание 2

```
cat /usr/local/bin/backup_home.sh
#!/bin/bash

# Скрипт зеркального резервного копирования домашней директории пользователя
# Дата и время для логов
DATE=$(date '+%Y-%m-%d %H:%M:%S')

# Пути
SRC="$HOME/"
DEST="/tmp/backup/"

# Выполнение rsync
rsync -av --delete --checksum --exclude='.*' "$SRC" "$DEST"
STATUS=$?

# Логирование результата в journald
if [ $STATUS -eq 0 ]; then
    /usr/bin/logger -t backup_home -p user.info "[$DATE] Резервное копирование успешно выполнено"
else
    /usr/bin/logger -t backup_home -p user.err "[$DATE] Ошибка при выполнении резервного копирования (код $STATUS)"
fi

exit $STATUS
```

```
crontab -l

0 2 * * * /usr/local/bin/backup_home.sh
```

<img width="853" height="384" alt="image" src="https://github.com/user-attachments/assets/37b49263-baab-4b5a-af8e-d38b465c8a77" />



---
