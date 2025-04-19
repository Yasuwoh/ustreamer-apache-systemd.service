# ustreamer-apache-systemd.service
systemd and apache configuration files using ustramer

# インストールの前に
必要に応じてパラメータを変更してください

## systemd/ustreamer-sock.service
- /dev/video0: カメラのデバイスファイル
- 1280x720: 映像の解像度

## apache2/ustreamer.conf
- /ustreamer/: ustreamerをサービスするロケーション
- /etc/apache2/digestpasswd: Digest認証ファイル
   - cf. `htdigest /etc/apache2/digestpasswd "ustreamer" <username>`

# インストール
## ustreamer ユーザを作ります
```
# useradd -G video ustreamer
```

## systemd ユニットファイルと apache2 コンフィグファイルを所定のディレクトリにコピーします。
```
# cp -i systemd/* /etc/systemd/system/
# cp -i apache2/* /etc/apache2/conf-available/
```

## ustreamer-sock サービスを有効化して開始します
```
# systemctl daemon-reload
# systemctl enable ustreamer-sock.service
# systemctl start ustreamer-sock.service
```

## ustreamer.conf を有効にして apache2 の設定を再読み込みします
```
# a2enconf ustreamer
# systemct reaload apache2.service
```

## アクセスしてみてください
http://localhost/ustreamer

