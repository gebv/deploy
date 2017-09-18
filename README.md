### Настройка

В файле inventory надо указать ip адрес сервера, куда деплоим приложение, а так-же пользователя и ключ для авторизации:

```
ansible_ssh_private_key_file = ~/.ssh/id-rsa
ansible_user = root

[all]
10.0.0.1
```

Кол-во инстансов приложений равно кол-ву портов в сonfig.yml
Названия файлов приложений должны совпадать с названиями в config.yml

```
---

- hosts: all
  become: yes
  become_method: sudo
  roles:
    - { role: common, app_user: app, app_group: app }
    - { role: deploy, app_user: app, app_group: app }
```


### Деплой

```
ansible-playbook -i inventory deploy.yml
```

### Шаблоны
Шаблоны для генерации конфигов находятся в каталогах

roles/deploy/templates:

```
app.service.j2       # systemd конфиг
config.json.j2       # release конфиг
nginx_upstream.j2    # nginx конфиг
```
