### Настраиваем бэкапы
#### Настроить стенд Vagrant с двумя виртуальными машинами server и client.

Настроить политику бэкапа директории /etc с клиента:
1) Полный бэкап - раз в день
2) Инкрементальный - каждые 10 минут
3) Дифференциальный - каждые 30 минут

Запустить систему на два часа. Для сдачи ДЗ приложить list jobs, list files jobid=<id>
и сами конфиги bacula
*Настроить доп. Опции - сжатие, шифрование, дедупликация*

### Домашняя работа.

####  Устанавливаем и настраиваем систему резервного копирования bacula.

  Для автоматического развертывания системы написана ansible-role. Большая часть переменных настраивается через описание в vars/main.yml в каждой роли.

  LZO обеспечивает гораздо более быструю компрессию и декомпрессию, но более низкую степень сжатия, чем GZIP. В нашем случае предпочтительнее использование более сильного сжатия.

  В папке dz приложены конфиги, а так же вывод по командам **bconsole**  >> list_jobs.log, list_files_jobid_1.log и list_files_jobid_10.log

```bash
├── dz
│   ├── config_client
│   │   ├── bacula-fd.conf
│   │   └── bconsole.conf
│   ├── config_server
│   │   ├── bacula-dir.conf
│   │   ├── bacula-sd.conf
│   │   └── bconsole.conf
│   ├── list_files_jobid_10.log
│   ├── list_files_jobid_1.log
│   └── list_jobs.log
```

##### Дерево роли Bacula

```bash
├── bacula-ansible
│   ├── ansible.cfg
│   ├── playbook.yml
│   ├── roles
│   │   ├── baculaclient
│   │   │   ├── tasks
│   │   │   │   └── main.yml
│   │   │   ├── templates
│   │   │   │   ├── bacula-fd.conf.j2
│   │   │   │   └── bconsole.conf.j2
│   │   │   └── vars
│   │   │       └── main.yml
│   │   ├── baculaserver
│   │   │   ├── tasks
│   │   │   │   └── main.yml
│   │   │   ├── templates
│   │   │   │   ├── bacula-dir.conf.j2
│   │   │   │   ├── bacula-sd.conf.j2
│   │   │   │   └── bconsole.conf.j2
│   │   │   └── vars
│   │   │       └── main.yml
│   │   ├── epel
│   │   │   └── tasks
│   │   │       └── main.yml
│   │   └── nginx
│   │       ├── handlers
│   │       │   └── main.yml
│   │       ├── tasks
│   │       │   └── main.yml
│   │       ├── templates
│   │       │   └── nginx.conf.j2
│   │       └── vars
│   │           └── main.yml
│   ├── staging
│   │   └── hosts
│   └── Vagrantfile
```  

### Краткая пямятка ручной установки
#### Установка bacula_server
```bash
yum -y install vim bacula-director bacula-storage bacula-console mariadb-server
```
```bash
vim /etc/my.cnf
alternatives --config libbaccats.so
systemctl start mariadb
systemctl enable mariadb
/usr/libexec/bacula/grant_mysql_privileges
/usr/libexec/bacula/create_mysql_database -u root
/usr/libexec/bacula/make_mysql_tables -u bacula
mysql_secure_installation
mysql -u root -p
mkdir -p /bacula/backup /bacula/restore
```
```bash
vim /etc/bacula/bacula-dir.conf
bacula-dir -tc /etc/bacula/bacula-dir.conf
vim /etc/bacula/bconsole.conf
vim /usr/libexec/bacula/make_catalog_backup.pl
systemctl start bacula-dir
systemctl enable bacula-dir
```
```bash
vim /etc/bacula/bacula-sd.conf
systemctl start bacula-sd
systemctl enable bacula-sd
```
```bash
bconsole
```
#### Установка bacula_client
```bash
yum -y install vim bacula-client bacula-console
```
```bash
vim /etc/bacula/bacula-fd.conf
systemctl start bacula-fd
systemctl enable bacula-fd
yum install mc wget httpd nano
```
