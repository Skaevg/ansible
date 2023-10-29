# Ansible
ansible-doc -l
ansible-doc [имя модуля]

Инвентарь

Может быть два расширения для инвентаря .ini .yaml
```
вариант.ini
my.domain.com
[mygroup]
domain.com
app.domain.com
[dbservers]
db.domain.com
```
```
.yaml
all:
    hosts:
        my.domain.com:
    children:
        mygroup:
            hosts:
                domain.com:
                app.domain.com:
        dbservers:
            hosts:
                db.domain.com:
```
так же можно указывать дополнительные списки серверов в .ini файлах
```
[webservers]
www.[01:50]example.com
```
использовать переменные 
```
[db]
mydb.ru env=productuon replicas=2
```
использовать alias (удобное обращение к хосту с портом по переменной coolhost)
```
[db]
coolhost ansible_port=2222 ansible_host=192.68.1.50
```

## Параметры подключения

```
ansible_connection
assible_host
ansible_port
ansible_user
ansible_password
```
Параметры ssh / scp / sftp
```
ansible_ssh_private_key_file
ansible_ssh_common_args
ansible_sftp_extra_args
ansible_scp_extra_args
ansible_ssh_extra_args
ansible_ssh_pipelining
ansible_ssh_executable
```
Привелегии (sudo)
```
ansible_become
ansible_become_method
ansible_become_user
ansible_become_password
ansible_become_exe
ansible_become_flags
```
Настройки shell
```
ansible_shell_type
ansible_python_interpreter
ansible_shell_executable
```

## Ad-hoc команды
для быстрых фиксов, без написания playbook 
```
ansible -i hosts -m user -a "name=alaricode state=present" all
          |         |                  |                    |
передаем хост       |                  |                    |
                    модуль             |                    |
                                   аргументы                |
                                                        указание хостов
```

Модули сервиса

```
ansible webservers -m service -a "name=httpd state=started"
ansible webservers -m command -a "/sbin/reboot -t now"
```