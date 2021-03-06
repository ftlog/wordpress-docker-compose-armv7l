# wordpress-docker-compose-armv7l

Docker Composeの公式サイトにある[yaml](https://docs.docker.jp/compose/wordpress.html)がRaspberry PIで動かなかったので修正しました。  
MySQLでは、armv7Lに対応したイメージが見つからなかったため、以下のmariadbイメージを使用しました。  
パスワードやDB名は適宜修正してください。  

linuxserver/mariadb  
https://hub.docker.com/r/linuxserver/mariadb  

## 動作確認環境
Raspberry PI 4 (Raspbian GNU/Linux 10)  
Docker version 19.03.13, build 4484c46 (docker/stable,now 1.5-2 all [インストール済み])  
docker-compose version 1.27.4, build 40524192  

## 使い方
1. git clone

    ```
    $ git clone https://github.com/ftlog/wordpress-docker-compose-armv7l
    ```

1. docker-compose.ymlをコピー

    ```
    $ mkdir /home/pi/docker-compose-file
    $ cp wordpress-docker-compose-armv7l/docker-compose.yml /home/pi/docker-compose-file
    ```

1. 起動

    ```
    $ cd /home/pi/docker-compose-file
    $ docker-compose up -d
    $ docker-compose ps
    ```
1. 停止

    ```
    $ docker-compose down
    ```
    データも含めて削除する場合は、
    ```
    $ docker-compose down --volumes
    ```

## (参考)Docker Composeのビルド
1. piユーザをdockerグループに追加

    ```
    $ sudo usermod -aG docker pi
    ```

1. docker-composeをgit clone  

    ```
    $ git clone https://github.com/docker/compose.git
    ```
    
1. docker-composeをビルド  

    ```
    $ python -m pip install --upgrade pip
    $ ./script/build/linux
    ```
  
1. docker-composeを/usr/local/binなどにコピー  

    ```
    $ cd dist/
    $ ls
    docker-compose-Linux-armv7l
    $ sudo cp docker-compose-Linux-armv7l /usr/local/bin/docker-compose
    $ sudo chown root.root /usr/local/bin/docker-compose
    $ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    $ docker-compose --version
    docker-compose version 1.27.4, build 40524192
    ```

## ライセンス

[MIT License](https://opensource.org/licenses/mit-license.php)
