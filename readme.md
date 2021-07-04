
Остановить все Docker контейнеры.

sudo docker stop $(docker ps -a -q)

Удалить все Docker контейнеры

sudo docker rm $(docker ps -a -q)

docker run -d -p 9000:9000 -v ~/.docker/machine/certs:/certs portainer/portainer -H tcp://192.168.99.100:2376 --tlsverify

  Install Docker for MX Linux 19
  Update the apt package index:

sudo apt-get update

  Install packages to allow apt to use a repository over HTTPS:

sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common

   Add Docker’s official GPG key:

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

    Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint:

sudo apt-key fingerprint 0EBFCD88

    Add stable repository:

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

    Update the apt package index:   

sudo apt-get update

    Install the latest version of Docker Engine - Community and containerd, or go to the next step to install a specific version:

sudo apt-get install docker-ce docker-ce-cli docker-compose containerd.io 

    This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits:

sudo docker run hello-world

    Manage containers with non-root user:

sudo groupadd docker && sudo usermod -aG docker $USER && newgrp docker
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

<http://localhost:9000>

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
