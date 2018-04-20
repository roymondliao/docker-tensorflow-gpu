# docker-tensorflow-gpu
dockerコンテナ上でtensorflow-gpuを動作させ、JupyterNotebookを立ち上げる。

## 動作環境
| ソフトウェア | バージョン |
|:---|:---|
| NVIDIAドライバ  | 384.111 |
| docker | 18.03.0-ce |
| docker-compose | 1.19.0-rc3 |
| nvidia-docker  | 2 |

## インストール
### NVIDIAのドライバ
[NVIDIAドライバダウンロード](http://www.nvidia.co.jp/Download/index.aspx?lang=jp)

    $ sudo service lightdm stop
    $ sudo ./NVIDIA-Linux-x86_64-384.111.run
    $ sudo reboot

### Docker
    $ sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    $ sudo apt-get update
    $ sudo apt-get -y install docker-ce

### docker-compose
    $ sudo curl -L https://github.com/docker/compose/releases/download/1.19.0-rc3/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    $ chmod +x /usr/local/bin/docker-compose

### dockerグループに追加
    $ sudo gpasswd -a ユーザ docker
再ログイン

### nvidia-docker2
    $ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey |   sudo apt-key add -
    $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
    $ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list |   sudo tee /etc/apt/sources.list.d/nvidia-docker.list
    $ sudo apt-get update
    $ sudo apt-get install -y nvidia-docker2
    $ sudo pkill -SIGHUP dockerd

## 動作手順
    $ git clone https://github.com/ubi-naist/docker-tensorflow-gpu.git
    $ cd docker-tensorflow-gpu
    $ cp .env.example .env
    $ nano .env
パスワードを変更 PASSWORD=XXXX

プロジェクト名を変更　COMPOSE_PROJECT_NAME=XXXX

    $ nano docker-compose.yml
ポート番号を変更 5000→XXXX

    $ docker-compose up
