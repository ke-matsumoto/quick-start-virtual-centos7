# quick-start-virtual-centos7
## 以下の環境で実施
-	Windows10
-	vagrant 2.3.4
-	virtualBox 6.1.44
## 事前インストール
- vagrant
    - https://developer.hashicorp.com/vagrant/downloads
- virtualBox
    - https://www.virtualbox.org/wiki/Download_Old_Builds_6_1
- Visual Studio Code (お好みのエディタがあればそちらをどうぞ)
    - https://azure.microsoft.com/ja-jp/products/visual-studio-code
- git bash
    - https://gitforwindows.org/
## git bashを起動、ビルド前の準備
### 必要なvagrantのプラグインをインストール
```
$ vagrant plugin install vagrant-omnibus
$ vagrant plugin install vagrant-vbguest
$ vagrant plugin install vagrant-hostmanager
```
### リポジトリの取得
```
$ cd /c
$ mkdir vagrant
$ cd vagrant
$ git clone git@github.com:ke-matsumoto/quick-start-virtual-centos7.git
```
## 仮想環境をビルド
### 仮想環境をビルド＆起動
```
$ cd /c/vagrant/quick-start-virtual-centos7
$ vagrant up
```
### ステータスがrunningか確認
```
$ vagrant status
```
## 以下 Docker Compose を利用する場合の手順
### dockerのインストール
#### install
```
$ vagrant ssh
[vagrant@localhost ~]$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
[vagrant@localhost ~]$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
[vagrant@localhost ~]$ sudo yum install -y docker-ce docker-ce-cli containerd.io
[vagrant@localhost ~]$ docker --version
Docker version 23.0.6, build ef23cbc
```
#### dockerデーモンの起動
```
[vagrant@localhost ~]$ sudo systemctl start docker
```
#### dockerのブート時自動起動を設定
```
[vagrant@localhost ~]$ sudo systemctl enable docker
```
#### dockerコマンドをsudoなしで実行できるよう設定
```
[vagrant@localhost ~]$ sudo groupadd docker
[vagrant@localhost ~]$ sudo gpasswd -a $USER docker
[vagrant@localhost ~]$ sudo systemctl restart docker
[vagrant@localhost ~]$ exit
$ vagrant ssh
```
#### 以下表示されること確認
```
[vagrant@localhost ~]$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```
### docker composeのインストール (2023/05/16時点 最新v2.17.3)
#### install
```
[vagrant@localhost ~]$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.17.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
[vagrant@localhost ~]$ sudo chmod +x /usr/local/bin/docker-compose
[vagrant@localhost ~]$ docker-compose --version
Docker Compose version v2.17.3
```
## 以下 GitHub を利用する場合の手順
### gitのインストール
#### install
```
[vagrant@localhost ~]$ sudo yum install git
[vagrant@localhost ~]$ git --version
git version 1.8.3.1
```
#### git configの設定
```
[vagrant@localhost ~]$ git config --global user.name 自身のGitアカウント名
[vagrant@localhost ~]$ git config --global user.email 自身のGitアカウントメールアドレス
[vagrant@localhost ~]$ git config --global color.ui true
```
### GitHubにSSHキー登録
- https://zenn.dev/cozftro/articles/2f841eaa83bd2a
## 以下 Visual Studio Code を利用する場合の手順
### Remote SSHの設定
- https://qiita.com/nlog2n2/items/1d1358f6913249f3e186
    - `[追記]VS Code で ssh-add 秘密鍵へのパスをしないと接続できない` はやらなくてもいけた
