Role Name
=========

Обертка над arillso.restic
Добавляет нужные директории и настройки файлового бекапа

Requirements
------------

* [python3](https://www.python.org/)
* python3-selinux (пакет в системе)
* jmespath (библиотека python)
* [docker](https://docs.docker.com/engine/install/)
* [ansible](https://docs.ansible.com/)
* [molecule](https://molecule.readthedocs.io) (+ molecule[docker])
* [arillso.restic](https://github.com/arillso/ansible.restic)

Пример установки

```bash
git clone git@github.com:antonpresn/backupfiles.git
cd backupfiles
python3 -m venv env
. env/bin/activate
python3 -m pip install --upgrade pip
pip install ansible
pip install molecule
pip install molecule[docker]
pip install jmespath
ansible-galaxy install arillso.restic


```

Role Variables
--------------
Те переменные, которые относятся к роли arillso.restic, описаны в репозитории роли (https://github.com/arillso/ansible.restic#role-variables)

Те переменные, которые обязательны для данной роли можно найти в файле vars/main.yml

```yaml
base_dir: '' # Директория сайта относительно которой производится бэкап
repo_location: '' # Размещение репозитория (url)
repo_password: '' # Пароль для репоизтория
aws_access_key: '' # Ключ для доступа к репозиторию в minio
aws_secret_access_key: '' # Ключ для доступа к репозиторию в minio
```

Dependencies
------------

Требует пакет jmespath

```bash
pip install jmespath
```

Для тестирования требует molecule, установка описана выше

Example Playbook
----------------


    - hosts: production-web
      collections:
        - learn.backupfiles
      tasks:
        - import_role:
              name: backup_files
      roles:
        - role: backup_files
          base_dir: '/var/www/prod'
          repo_location: "s3:http://{{ repo_location }}:9000"
          repo_password: '{{ backup_files_repo_password }}'
          aws_access_key: '{{ aws_root_user }}'
          aws_secret_access_key: '{{ aws_root_password }}'

License
-------

BSD

Testing
-------

```bash
cd backup_files
molecule test
```
