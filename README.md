<h1>Nginxを利用した、簡単に建てられるRTMPサーバー</h1>
<br />
<p>
動作環境：
　Ubuntu20.04 amd64(さくらのVPS 512MB)
<br/>
パケットフィルター設定：
<br/>
　SSH TCP22 すべて許可する
<br/>
　Web TCP80 / 443 すべて許可する
<br/>
　カスタム RCP1935 すべて許可する
</p>

ソフトウェアアップデート

```

sudo apt update

```

ファイアウォールの設定

```

sudo ufw enable

sudo ufw allow 22

sudo ufw allow 80

sudo ufw allow 443

sudo ufw allow 1935

```

<h3>
  Nginx-1.17.10とnginx-rtmp-moduleのインストール
</h3>
<a href="https://github.com/arut/nginx-rtmp-module/wiki/Getting-started-with-nginx-rtmp#set-up-live-streaming">引用元
</a>
ビルドユーティリティのインストール

```

sudo apt-get install build-essential libpcre3 libpcre3-dev libssl-dev git zlib1g-dev -y

```

ビルドディレクトリ（ホーム）を作成して作業ディレクトリを設定

```

sudo mkdir ~/build && cd ~/build

```

最新の nginx-rtmp をダウンロードして解凍する

```

sudo git clone http://github.com/arut/nginx-rtmp-module.git

```

nginxのダウンロードと解凍

```

sudo wget http://nginx.org/download/nginx-1.17.10.tar.gz

sudo tar xzf nginx-1.17.10.tar.gz

cd nginx-1.17.10

```

nginx-rtmp で nginx をビルドする

```

sudo ./configure --with-http_ssl_module --add-module=../nginx-rtmp-module

```

ステータスモジュールが必要な場合

```

sudo ./configure --with-http_ssl_module --add-module=../nginx-rtmp-module --with-http_stub_status_module --with-debug --with-cc-opt="-Wimplicit-fallthrough=0"

```

nginxのインストール

```

sudo make

sudo make install

```

サーバーを起動

```

sudo /usr/local/nginx/sbin/nginx

```

<p>
  この時点でサイトにアクセスし、「Welcome to nginx!」と表示されれば成功
</p>

サーバーの停止

```

sudo /usr/local/nginx/sbin/nginx -s stop

```

不要ファイルの移動(old-**)

```

cd /usr/local/nginx/

sudo mv html old-html

sudo mv conf old-conf

```

<h3>
  Live-stream-server-portable-Windows-Nginx-RTMP-HLS-Dashのダウンロード
</h3>

```

sudo git clone https://github.com/ustoopia/Live-stream-server-portable-Windows-Nginx-RTMP-HLS-Dash.git

```

各ファイルの移動

```

sudo mv Live-stream-server-portable-Windows-Nginx-RTMP-HLS-Dash RTMP-server

sudo mv RTMP-server/conf conf

sudo mv RTMP-server/html site

sudo mv RTMP-server/logs logs

sudo mv RTMP-server/recordings recordings

sudo mv RTMP-server/temp temp

```

サーバーの起動

```

sudo /usr/local/nginx/sbin/nginx

```

使用法は、<a href="https://github.com/ustoopia/Live-stream-server-portable-Windows-Nginx-RTMP-HLS-Dash">こちら</a>を参照してください。

