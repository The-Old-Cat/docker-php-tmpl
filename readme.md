


Остановить все Docker контейнеры.

sudo docker stop $(docker ps -a -q)


Удалить все Docker контейнеры

sudo docker rm $(docker ps -a -q)


docker run -d -p 9000:9000 -v ~/.docker/machine/certs:/certs portainer/portainer -H tcp://192.168.99.100:2376 --tlsverify



install Docker

First, download and add Docker CE GPG key with the following command:

wget https://download.docker.com/linux/ubuntu/gpg
sudo apt-key add gpg


Next, add the Docker CE repository to APT with the following command:

sudo gedit /etc/apt/sources.list.d/docker.list



Add the following line:

deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable



Save and close the file, when you are finished. Then, update the repository with the following command:

sudo apt-get update -y



Once the repository is updated, install Docker CE with the following command:

sudo apt-get install docker-ce -y
sudo apt-get install docker

After installing Docker CE, check the Docker service with the following command:

sudo systemctl status docker


Run this command to download the current stable release of Docker Compose

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

docker-compose --version




Как установить Docker Portainer

Для выполнения этой статьи вам понадобится уже установленный в вашей системе Docker. Я не буду подробно рассказывать как установить docker и docker-compose.

После того, как Docker будет установлен, можно развернуть контейнер с Portainer. Было бы странно, если бы программа поставлялась в каком-либо другом виде. Создайте хранилище данных для Portainer:

docker volume create portainer_data

Для установки и запуска контейнера выполните:

docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

Эта команда настраивает автоматический запуск Portainer после перезагрузки, а также постоянное хранилище, чтобы ваши настройки не потерялись при удалении и повторном разворачивании контейнера. Чтобы убедится, что Portainer запущен выполните такую команду:

docker ps
Настройка Portainer
1. Вход

Получить доступ к программе вы можете через веб-интерфейс на порту 9000. Откройте его в браузере. На первом шаге надо будет ввести имя пользователя и пароль, под которым вы будете входить в систему:

Затем выберите метод подключения к Docker. Для начала можно подключиться к локальному сервису Docker. Для этого выберите Local:


Как обновить Portainer

Чтобы обновить Portainer надо удалить текущий образ и запустить его снова. Это не вызовет никаких проблем, так как при создании предыдущего образа мы использовали внешнее хранилище для хранения данных. Остановите образ и удалите его:

docker stop portainer

docker rm portainer

Скачайте новую версию:

docker pull portainer/portainer

Затем осталось снова установить Portainer:

docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
После того, как Docker будет установлен, можно развернуть контейнер с Portainer. Было бы странно, если бы программа поставлялась в каком-либо другом виде. Создайте хранилище данных для Portainer:

docker volume create portainer_data

Для установки и запуска контейнера выполните:

docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

Чтобы убедится, что Portainer запущен выполните такую команду:

docker ps

http://localhost:9000

Остановить все Docker контейнеры.

sudo docker stop $(docker ps -a -q)


Удалить все Docker контейнеры

sudo docker rm $(docker ps -a -q)

добовляем пользователя и группу docker
sudo groupadd docker
sudo usermod -aG docker $USER


docker-shop-webdevkin
phpmyadmin 
localhost:8001


127.0.0.1 нужно заменить на адрес виртуальной машины, в которой запускается докер, 