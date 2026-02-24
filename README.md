# Домашнее задание к занятию 3 «Использование Ansible» Павлов Дмитрий  

## 0. Подготовьте в Yandex Cloud три хоста: для clickhouse, для vector и для lighthouse.  
![Подготовка ВМ](/pic/pic01.png)  
![Подготовка ВМ](/pic/pic02.png)  
## 1.Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.  
## 2.При создании tasks рекомендую использовать модули: get_url, template, yum, apt.  
## 3. Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.  
## 4.Подготовьте свой inventory-файл prod.yml.  
## 5. Запустите ansible-lint site.yml и исправьте ошибки, если они есть.  
![Задание 5](/pic/pic03.png)  
## 6. Попробуйте запустить playbook на этом окружении с флагом --check.  
![Задание 6](/pic/pic04.png)
## 7. Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.  
![Задание 7](/pic/pic05-01.png)
![Задание 7](/pic/pic05-02.png)
## 8. Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.  
![Задание 8](/pic/pic06.png)  
![Проверка что все устаноилось](/pic/pic07.png)  
## 9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.  

## Параетры: ./roles/lighthouse/vars/main.yml  
```
---
lighthouse_repo: "https://github.com/VKCOM/lighthouse.git" - Репозитарий который берем
lighthouse_version: "master" - ветка с которой берем

lighthouse_src_dir: "/opt/lighthouse" - создаем директорию куда будем копировать исходники из гита
lighthouse_root: "/var/www/lighthouse" - сюда их перенесем после копирования

nginx_listen_port: 80
nginx_server_name: "_"
```
## Теги: lighthouse, nginx  
```
./roles/lighthouse/tasks$ cat main.yml 
---
- name: Install required packages
  ansible.builtin.apt:
    name:
      - nginx
      - git
      - rsync
    state: present
    update_cache: true
    cache_valid_time: 3600
    lock_timeout: 300
  tags: [lighthouse, nginx]

```

## 10.Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-03-yandex на фиксирующий коммит, в ответ предоставьте ссылку на него.  