# Установка

### Установка ansible (v. 1.9.x)

*CentOS 6*

```
sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
sudo yum install -y gcc python-pip python-devel git openssl-devel libffi-devel libselinux-python
sudo pip install ansible
```

*CentOS 7*

```
sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum install -y gcc python-pip python-devel git openssl-devel libffi-devel
sudo pip install ansible
```

*Ubuntu*

```
sudo apt-get -y update
sudo apt-get -y install git python-pip python-dev libffi-dev python-markupsafe libssl-dev
sudo pip install ansible
```

# Сценарии

- *lamp.yml*
nginx + apache + mysql + php5.6. 

Пример установки:

```
ansible-playbook -e @config/main.json -c local -i inventory lamp.yml
```

- *lemp.yml* 
nginx + mysql + php5.6.

Пример установки:

```
ansible-playbook -e @config/main.json -c local -i inventory lemp.yml
```

- *lemp7.yml*
nginx + mysql + php7.0.

Пример установки: 

```
ansible-playbook -e @config/main.json -c local -i inventory_php7 lemp7.yml
```

- *lvemp7.yml*
varnish + nginx + mysql + php7.0.

Пример установки: 

```
ansible-playbook -e @config/main.json -c local -i inventory_varnish lvemp7.yml
```

В Ubuntu возможны проблемы при установке php7

*Стабильно работает только на чистых инсталляциях.*

### Запуск плейбука

1. Скачиваем репозиторий. 
```
mkdir ~/playbooks && git clone https://github.com/cscart/server-ansible-playbooks ~/playbooks
```

2. Настройка
```
cp ~/playbooks/config/advanced.json  ~/playbooks/config/main.json
```
 Вносим правки в файл ~/playbooks/config/main.json.
 - stores_dir - директория проектов
 - stores - массив проектов
    - «example.com» - доменное имя проекта
    - storefronts - массив доменных имен витрин, если таких не имеется то нужно оставить поле пустым. Пример: "storefronts": []
    - database - параметры подключения к БД. Нельзя использовать user root, так как это вызовет проблемы с доступом к базам самого пользователя root.

3. Запуск
```
cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory lamp.yml
```

Если процесс прошел успешно, то можно устанавливать cscart.
