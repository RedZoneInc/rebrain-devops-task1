# Nginx ![](https://www.andreyus.com/wp-content/uploads/2019/08/NGINX-logo-rgb-large-1024x344.png)
**Nginx [engine x]** — это **HTTP-сервер** и **обратный прокси-сервер**, **почтовый прокси-сервер**, а также **TCP/UDP прокси-сервер общего назначения**, изначально написанный [**Игорем Сысоевым**](https://ru.wikipedia.org/wiki/%D0%A1%D1%8B%D1%81%D0%BE%D0%B5%D0%B2,_%D0%98%D0%B3%D0%BE%D1%80%D1%8C_%D0%92%D0%BB%D0%B0%D0%B4%D0%B8%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B8%D1%87_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%81%D1%82)). Уже длительное время он обслуживает серверы многих высоконагруженных российских сайтов, таких как [Яндекс](https://yandex.ru/), [Mail.Ru](https://mail.ru/), [ВКонтакте](https://vk.com/) и [Рамблер](https://www.rambler.ru/). [Согласно статистике Netcraft](https://news.netcraft.com/archives/category/web-server-survey/) - **nginx** обслуживал или проксировал **25.58%** самых нагруженных сайтов в **июле 2020 года**. 

Вот некоторые примеры успешного внедрения **nginx**: *[Dropbox](https://www.dropbox.com/ru/), [Netflix](https://www.netflix.com/ru/), [Wordpress.com](https://ru.wordpress.com/), [FastMail.FM](https://www.fastmail.com/login/?domain=fastmail.fm)*

Протестированные ОС и платформы, поддерживающие установку "Nginx"
----
* FreeBSD 3 — 12 / i386; FreeBSD 5 — 12 / amd64; FreeBSD 11 / ppc; FreeBSD 12 / ppc64;
* Linux 2.2 — 4 / i386; Linux 2.6 — 5 / amd64; Linux 3 — 4 / armv6l, armv7l, aarch64, ppc64le;
* Solaris 9 / i386, sun4u; Solaris 10 / i386, amd64, sun4v; Solaris 11 / x86;
* AIX 7.1 / powerpc;
* HP-UX 11.31 / ia64;
* macOS / ppc, i386, x86_64;
* Windows XP, Windows Server 2003, Windows 7, Windows 10.

Инструкции по установке
----
Для того, чтобы поставить **nginx** на новой машине, необходимо подключить и настроить репозиторий пакетов **nginx**. После этого можно будет установить и обновлять **nginx** из этого репозитория.

#### [RHEL/CentOS]
Установите пакеты, необходимые для подключения **yum-репозитория**:

```
sudo yum install yum-utils
```
Для подключения **yum-репозитория** создайте файл с именем */etc/yum.repos.d/nginx.repo* со следующим содержимым:
```
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=1
enabled=0
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
```

По умолчанию используется репозиторий для стабильной версии **nginx**. Если предпочтительно использовать пакеты для основной версии **nginx**, выполните следующую команду:
```
sudo yum-config-manager --enable nginx-mainline
```
Чтобы установить **nginx**, выполните следующую команду:
```
sudo yum install nginx
```
При запросе подтверждения GPG-ключа проверьте, что отпечаток ключа совпадает с **573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62**, и, если это так, подтвердите его.

#### [Debian]
Установите пакеты, необходимые для подключения **apt-репозитория**:
```
sudo apt install curl gnupg2 ca-certificates lsb-release
```
Для подключения **apt-репозитория** для стабильной версии **nginx**, выполните следующую команду:

```
echo "deb http://nginx.org/packages/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
```
Если предпочтительно использовать пакеты для основной версии **nginx**, выполните следующую команду вместо предыдущей:
```
echo "deb http://nginx.org/packages/mainline/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
```    
Теперь нужно импортировать официальный ключ, используемый **apt** для проверки подлинности пакетов:
```
curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -
```
Проверьте, верный ли ключ был импортирован:
```
sudo apt-key fingerprint ABF5BD827BD9BF62
```
Вывод команды должен содержать полный отпечаток ключа **573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62**:
```
pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573B FD6B 3D8F BC64 1079  A6AB ABF5 BD82 7BD9 BF62
uid   [ unknown] nginx signing key <signing-key@nginx.com>
```
Чтобы установить **nginx**, выполните следующие команды:
```
sudo apt update
sudo apt install nginx
```

#### [Ubuntu]

Установите пакеты, необходимые для подключения **apt-репозитория**:
```
sudo apt install curl gnupg2 ca-certificates lsb-release
```
Для подключения **apt-репозитория** для стабильной версии **nginx**, выполните следующую команду:
```
echo "deb http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
```
Если предпочтительно использовать пакеты для основной версии **nginx**, выполните следующую команду вместо предыдущей:
```
echo "deb http://nginx.org/packages/mainline/ubuntu `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
```
Теперь нужно импортировать официальный ключ, используемый **apt** для проверки подлинности пакетов:
```
curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -
```
Проверьте, верный ли ключ был импортирован:
```
sudo apt-key fingerprint ABF5BD827BD9BF62
```

Вывод команды должен содержать полный отпечаток ключа **573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62**:
```
pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573B FD6B 3D8F BC64 1079  A6AB ABF5 BD82 7BD9 BF62
uid   [ unknown] nginx signing key <signing-key@nginx.com>
```
Чтобы установить **nginx**, выполните следующие команды:

```
sudo apt update
sudo apt install nginx
```

Запуск, перезапуск и остановка nginx используя systemctl
----
SystemD - это менеджер системы и служб для последних выпусков **Ubuntu 20.04 / 18.04 / 16.04, CentOS 7/8 и Debian 10/9**.

Всякий раз, когда вы вносите изменения в конфигурацию **nginx**, вам необходимо перезапустить или перезагрузить процессы веб-сервера. Выполните следующую команду, чтобы перезапустить службу **nginx**:
```
sudo systemctl restart nginx
or
sudo systemctl reload nginx
```
При добавлении или редактировании серверных блоков предпочитайте перезагрузку, а не перезапуск. Перезапускайте службу только при внесении значительных изменений, таких как изменение портов или интерфейсов. При перезагрузке **nginx** загружает новую конфигурацию, запускает новые рабочие процессы с новой конфигурацией и корректно завершает работу старых рабочих процессов.

Выполните команду ниже, чтобы перезагрузить службу **nginx**:
```
sudo systemctl reload nginx
```
**nginx** также может напрямую контролироваться с помощью сигналов. Например, чтобы перезагрузить сервис, вы можете использовать следующую команду:
```
sudo /usr/sbin/nginx -s reload
```
Чтобы запустить службу **nginx**, выполните следующую команду:
```
sudo systemctl start nginx
```
Выполните следующую команду, чтобы остановить службу **nginx**:
```
sudo systemctl stop nginx
```

Запуск, перезапуск и остановка Nginx используя SysVinit
----
Старые (**EOLed**) версии **Ubuntu**, **CentOS** и **Debian** используют сценарии **init.d** для запуска, остановки и перезапуска демона **nginx**.

Выполните команду ниже, чтобы перезапустить службу **nginx**:
```
sudo service nginx restart
```
Выполните команду ниже, чтобы перезагрузить службу **nginx**:
```
sudo service nginx reload
```
Чтобы запустить службу **nginx**, выполните следующую команду:
```
sudo service nginx start
```
Выполните следующую команду, чтобы остановить службу **nginx**:
```
sudo service nginx stop
```

Проверка работоспособности сервера через браузер
----
Перейдите по ссылке в браузере http://your-server-ip-address:80/
Если сервер был установлен и запущен правильно, то в браузере вы должны увидеть **страницу по умолчанию** сервера **nginx**:
![](https://live.staticflickr.com/2829/12112587324_c2bb7b3338_z.jpg)

Больше информации о управлении службой **nginx**, настройках конфигурационного файла сервера можно узнать в [руководстве для начинающих](https://nginx.org/ru/docs/beginners_guide.html) или в [технической документации](https://nginx.org/ru/docs/).

Авторы
----
[**Игорь Сысоев**](https://ru.wikipedia.org/wiki/%D0%A1%D1%8B%D1%81%D0%BE%D0%B5%D0%B2,_%D0%98%D0%B3%D0%BE%D1%80%D1%8C_%D0%92%D0%BB%D0%B0%D0%B4%D0%B8%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B8%D1%87_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%81%D1%82))

Версии
----
Скачать необходимую версию можно [здесь](https://nginx.org/ru/download.html).

Лицензия
----
Исходные тексты и документация проекта распространяются под [BSD-подобной лицензией](https://ru.wikipedia.org/wiki/%D0%9B%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D1%8F_BSD) из 2 пунктов.

Ссылки
----
* Домашняя страница: https://nginx.org/ru/
* Заргузки: [.tar.gz](https://nginx.org/download/nginx-1.19.1.tar.gz) или [.zip](https://nginx.org/download/nginx-1.19.1.zip)
* Новости: https://nginx.org/
* Документация: https://nginx.org/ru/docs/
* Техподдержка: https://nginx.org/en/support.html
* Часто задаваемые вопросы (FAQ): https://nginx.org/en/docs/faq.html
* Исходный код: https://trac.nginx.org/nginx/browser
* Твиттер: [@nginxorg](https://twitter.com/nginxorg)
* [Скриншоты](https://www.google.com/search?q=nginx+screenshots&newwindow=1&sxsrf=ALeKk01vxHYhNaNLUNbpAlV5Op1CQMvu7w:1596407158966&source=lnms&tbm=isch&sa=X&ved=2ahUKEwjj34GNyP3qAhXpwosKHe_KCkkQ_AUoAXoECA4QAw&biw=2560&bih=1297)
