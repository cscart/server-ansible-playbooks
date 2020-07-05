# Configure Environment for CS-Cart/Multi-Vendor

These Ansible playbooks will configure the web server for CS-Cart or Multi-Vendor automatically. It will only take a few commands and adjustments to the configuration file.

**The playbooks were developed for clean OS installations.**


## Step 1. Install Ansible (v. 2.4.x)

*CentOS 6*

```
sudo yum -y install epel-release
sudo yum install -y gcc git openssl-devel libffi-devel libselinux-python python-crypto python-jinja2 python-paramiko sshpass python-six PyYAML
sudo rpm -ihv https://releases.ansible.com/ansible/rpm/release/epel-6-x86_64/ansible-2.4.6.0-1.el6.ans.noarch.rpm
```

*CentOS 7*

```
sudo yum -y install epel-release
sudo yum install -y gcc git openssl-devel libffi-devel libselinux-python python-crypto python-jinja2 python-paramiko sshpass PyYAML python-setuptools
sudo rpm -ihv  https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.4.6.0-1.el7.ans.noarch.rpm
```

*Ubuntu 14.04*

```
sudo add-apt-repository -y ppa:ansible/ansible-2.4
sudo apt-get -y update
sudo apt-get -y install git python-dev libffi-dev python-markupsafe libssl-dev
sudo apt-get -y install ansible
```

*Ubuntu 16.04*

```
sudo add-apt-repository -y ppa:ansible/ansible-2.4
sudo apt-get -y update
sudo apt-get -y install git python-dev libffi-dev python-markupsafe libssl-dev
sudo apt-get -y install ansible
```

*Ubuntu 18.04*

```
sudo apt update
sudo apt install ansible
```

In the case you're using an remote MySQL instance, you'll need this on your controller node too.
```
sudo apt install python-mysqldb
```

## Step 2. Configure main.json

1. Clone the repository: 

   ```
   mkdir ~/playbooks && git clone https://github.com/cscart/server-ansible-playbooks ~/playbooks
   ```

2. Create **main.json**:

   ```
   cp ~/playbooks/config/advanced.json  ~/playbooks/config/main.json
   ```

3. Edit **~/playbooks/config/main.json**:

   * `stores_dir` - your project directory
   * `stores` - an array of projects
     * `example.com` - the domain name of a project
     * `storefronts` - an array with the domain names of the storefronts. If there are no storefronts, leave the array empty. For example: `"storefronts": []`
     * `database` - the credentials of the database that will be created by the playbook. **DON'T** set `root` as a user here, or else `root` won't be able to access or create any other databases.


## Step 3. Run a Playbook

Run **one of the playbooks** by using a command below. If there are no errors, you can install CS-Cart or Multi-Vendor after that.

* **lamp.yml**: nginx + apache + mysql + php5.6

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory lamp.yml
  ```

* **lemp.yml**: nginx + mysql + php5.6.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory lemp.yml
  ```

* **lemp7.yml**: nginx + mysql + php7.1.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory_php7 lemp7.yml
  ```

* **lvemp7.yml**: varnish + nginx + mysql + php7.1.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory_varnish lvemp7.yml
  ```


---

# Настройка окружения для CS-Cart/Multi-Vendor

Эти плейбуки для Ansible автоматически настроят веб-сервер для CS-Cart или Multi-Vendor. От вас потребуется выполнить несколько команд и указать настройки в одном файле.

**Плейбуки работает стабильно только на чистых инсталляциях операционных систем.**

## Шаг 1. Установка Ansible (v. 2.4.x)

*CentOS 6*

```
sudo yum -y install epel-release
sudo yum install -y gcc git openssl-devel libffi-devel libselinux-python python-crypto python-jinja2 python-paramiko sshpass python-six PyYAML
sudo rpm -ihv https://releases.ansible.com/ansible/rpm/release/epel-6-x86_64/ansible-2.4.6.0-1.el6.ans.noarch.rpm
```

*CentOS 7*

```
sudo yum -y install epel-release
sudo yum install -y gcc git openssl-devel libffi-devel libselinux-python python-crypto python-jinja2 python-paramiko sshpass  PyYAML python-setuptools
sudo rpm -ihv  https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.4.6.0-1.el7.ans.noarch.rpm
```

*Ubuntu 14.04*

```
sudo add-apt-repository -y ppa:ansible/ansible-2.4
sudo apt-get -y update
sudo apt-get -y install git python-dev libffi-dev python-markupsafe libssl-dev
sudo apt-get -y install ansible
```

*Ubuntu 16.04*

```
sudo add-apt-repository -y ppa:ansible/ansible-2.4
sudo apt-get -y update
sudo apt-get -y install git python-dev libffi-dev python-markupsafe libssl-dev
sudo apt-get -y install ansible
```


## Шаг 2. Настройка main.json

1. Скачиваем репозиторий.

   ```
   mkdir ~/playbooks && git clone https://github.com/cscart/server-ansible-playbooks ~/playbooks
   ```

2. Создаем **main.json**:

   ```
   cp ~/playbooks/config/advanced.json  ~/playbooks/config/main.json
   ```

3. Вносим правки в **~/playbooks/config/main.json**:
   * `stores_dir` - директория проектов
   * `stores` - массив проектов
     * `example.com` - доменное имя проекта
     * `storefronts` - массив доменных имен витрин; если таких не имеется, оставьик поле пустым. Пример: `"storefronts": []`
     * `database` - параметры подключения к БД, которую создаст плейбук. **НЕЛЬЗЯ** указывать пользователя `root`; если укажете, то `root` сможет пользоваться только базой, созданной плейбуком, и не сможет создавать новые БД.


## Шаг 3. Запуск плейбука

Запустите **один из плейбуков** с помощью соответствующей команды. Если процесс пройдет успешно, то можно будет устанавливать CS-Cart или Multi-Vendor.

* **lamp.yml**: nginx + apache + mysql + php5.6

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory lamp.yml
  ```

* **lemp.yml**: nginx + mysql + php5.6.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory lemp.yml
  ```

* **lemp7.yml**: nginx + mysql + php7.1.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory_php7 lemp7.yml
  ```

* **lvemp7.yml**: varnish + nginx + mysql + php7.1.

  ```
  cd ~/playbooks/ && ansible-playbook -e @config/main.json -c local -i inventory_varnish lvemp7.yml
  ```
