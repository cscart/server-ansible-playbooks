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

Для php7, поддерживаемые ос:

- Ubuntu 14.04 x86_64
- Ubuntu 15.04 x86_64
- CentOS 6 x86_64
- CentOS 7 x86_64

*Стабильно работает только на чистых инсталляциях.*


# Установка

### Установка ansible (v. 1.9.x)

*Ubuntu*

```
sudo apt-get -y update
sudo apt-get -y install git python-pip python-dev
sudo pip install ansible
```

*CentOS 6*

```
sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
sudo yum install -y gcc python-pip python-devel git
sudo pip install ansible
```

*CentOS 7*

```
sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum install -y gcc python-pip python-devel git
sudo pip install ansible
```

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
    - storefronts - массив доменных имен витрин
    - database - параметры подключения к БД

3. Запуск
```
cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory_varnish lvemp7.yml
```

Если процесс прошел успешно, то можно устанавливать cscart.
