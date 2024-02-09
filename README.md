# PAM

- Запретить всем пользователям, кроме группы admin логин в выходные (суббота и воскресенье), без учета праздников


- использован модуль pam_exec.so и написан скрипт [pam_script.sh](./pam_script.sh)
- создан тестовый пользователь test_admin входящий в группу admin

> Для выполнения ДЗ был использован Centos 8

## Проверка

- для начала попробуем залогиниться пользователем vagrant

```bash
ssh -o IdentitiesOnly=yes vagrant@127.0.0.1 -p 2222
vagrant@127.0.0.1's password: 
/usr/local/bin/pam_script.sh failed: exit code 1
Connection closed by 127.0.0.1 port 2222
```

> Нас постигнет неудача, т.к. сегодня воскресенье

- теперь попробуем залогиниться пользователем test_admin входящим в группу admin

```bash
ssh -o IdentitiesOnly=yes test_admin@127.0.0.1 -p 2222
test_admin@127.0.0.1's password:
[test_admin@PAM ~]$
```

> Успех
