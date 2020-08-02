# Nginx ![](https://www.andreyus.com/wp-content/uploads/2019/08/NGINX-logo-rgb-large-1024x344.png)
**nginx [engine x]** — это **HTTP-сервер** и обратный прокси-сервер, почтовый прокси-сервер, а также TCP/UDP прокси-сервер общего назначения, изначально написанный [*Игорем Сысоевым*](https://ru.wikipedia.org/wiki/%D0%A1%D1%8B%D1%81%D0%BE%D0%B5%D0%B2,_%D0%98%D0%B3%D0%BE%D1%80%D1%8C_%D0%92%D0%BB%D0%B0%D0%B4%D0%B8%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B8%D1%87_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%81%D1%82)). Уже длительное время он обслуживает серверы многих высоконагруженных российских сайтов, таких как [Яндекс](https://yandex.ru/), [Mail.Ru](https://mail.ru/), [ВКонтакте](https://vk.com/) и [Рамблер](https://www.rambler.ru/). [Согласно статистике Netcraft](https://news.netcraft.com/archives/category/web-server-survey/) - **nginx** обслуживал или проксировал **25.58%** самых нагруженных сайтов в **июле 2020 года**. Вот некоторые примеры успешного внедрения **nginx**: *Dropbox, Netflix, Wordpress.com, FastMail.FM.*

Исходные тексты и документация распространяются под BSD-подобной лицензией из 2 пунктов.

Коммерческая поддержка осуществляется компанией [**Nginx, Inc.**](https://nginx.org/ru/)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Installing

### Инструкции по установке
Для того, чтобы поставить **nginx** на новой машине, необходимо подключить и настроить репозиторий пакетов **nginx**. После этого можно будет установить и обновлять **nginx** из этого репозитория.

#### RHEL/CentOS
Установите пакеты, необходимые для подключения yum-репозитория:

```
sudo yum install yum-utils
```
Для подключения yum-репозитория создайте файл с именем */etc/yum.repos.d/nginx.repo* со следующим содержимым:
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
Чтобы установить nginx, выполните следующую команду:
```
sudo yum install nginx
```
При запросе подтверждения GPG-ключа проверьте, что отпечаток ключа совпадает с **573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62**, и, если это так, подтвердите его.

#### Debian
Установите пакеты, необходимые для подключения apt-репозитория:
```
sudo apt install curl gnupg2 ca-certificates lsb-release
```
Для подключения apt-репозитория для стабильной версии **nginx**, выполните следующую команду:

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

#### Ubuntu

Установите пакеты, необходимые для подключения apt-репозитория:
```
sudo apt install curl gnupg2 ca-certificates lsb-release
```
Для подключения apt-репозитория для стабильной версии **nginx**, выполните следующую команду:
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

pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573B FD6B 3D8F BC64 1079  A6AB ABF5 BD82 7BD9 BF62
uid   [ unknown] nginx signing key <signing-key@nginx.com>

Чтобы установить **nginx**, выполните следующие команды:

```
sudo apt update
sudo apt install nginx
```


## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
