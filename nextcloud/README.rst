Install Nextcloud di Raspberry Pi via Docker
=================================================================================

.. contents:: Daftar Isi

Install
---------------------------------------------------------------------------------

Install nextcloud via docker dengan docker-compose.yml sebagai berikut:

::

    version: '2'

    volumes:
      nextcloud:
      db:

    services:
      db:
        image: mariadb
        restart: always
        command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
        volumes:
          - db:/var/lib/mysql
        environment:
          - MYSQL_ROOT_PASSWORD=
          - MYSQL_PASSWORD=
          - MYSQL_DATABASE=nextcloud
          - MYSQL_USER=nextcloud

      app:
        image: nextcloud
        restart: always
        ports:
          - 8080:80
        links:
          - db
        volumes:
          - nextcloud:/var/www/html
        environment:
          - MYSQL_PASSWORD=
          - MYSQL_DATABASE=nextcloud
          - MYSQL_USER=nextcloud
          - MYSQL_HOST=db

**Referensi**

`nextcloud docker <https://hub.docker.com/_/nextcloud>`_

Client
---------------------------------------------------------------------------------

Data yang disimpan di server bisa disinkronisasi dengan aplikasi client.
Aplikasi tersebut tersedia untuk Windows 10, macOS, Linux, Android, dan iOS.

Install di Ubuntu
*********************************************************************************

::

    sudo add-apt-repository ppa:nextcloud-devs/client
    sudo apt-get update
    sudo apt install nextcloud-desktop

**Referensi**

`desktop client nextcloud - ppa <https://launchpad.net/~nextcloud-devs/+archive/ubuntu/client>`_

Notes
---------------------------------------------------------------------------------

Data dari client app disimpan di sebuah folder di lokal komputer. Folder tersebut dapat dijadikan sebuah git repo.


