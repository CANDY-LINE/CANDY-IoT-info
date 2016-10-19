[🔙目次ページへ戻る](README.md)

## CANDY IoT向けEdisonのセットアップ

[CANDY IoT](http://www.candy-line.io/proandsv.html#candyiot)に接続されたEdisonをセットアップしましょう。この手順は、ファームウェアを入れ直した場合に、LTEモジュール向け設定などがなくなってしまった時に、必要なソフトウェアなどを設定するためのものです。

ファームウェアの更新方法については、こちらではなく[Edisonファームウェア更新方法](Edisonファームウェア更新方法.md)に記載していますのでご覧ください。

### Edisonをコンソールから動かす

パソコンに、[CANDY IoT](http://www.candy-line.io/proandsv.html#candyiot)を接続しましょう。

Linux/macOSの場合は、以下のコマンドを入力するとターミナルからEdisonのコンソールを動かせるようになります。

```
screen ポート 115200
```

ポートには、Linuxの場合は、`ls /dev/ttyUSB*`を実行して、表示されたパスを入力して接続されたものを使用します。もし、何の反応もない場合は、エンターを押してみてください。それでも反応がない場合は、`Ctrl+A+\`を押して、screenコマンドを終了し、次のパスをお試しください。

macOSの場合は、`ls /dev/tty.usbserial*`を実行して、同じように表示されたパスを1つずつおためしください。

Windowsの場合は、Tera TermやPuttyを利用して、利用できるCOMポートを探して接続してください。ボーレートは 115200 bps で、それ以外の設定はデフォルトで動作します。

### Edisonへのログイン

ファームウェアを入れ替えたばかりの状態では、ログインは、`root`ユーザーで入ります。パスワードは設定されていないので、ユーザーIDを指定するとそのままログイン出来ます。

### Wi-FiとSSHの設定

この状態では、何もセットアップできないので、Wi-FiとSSHを設定しましょう。コンソールから以下のコマンドを入力して実行します。

```
configure_edison --wifi
```

【注意】[CANDY IoT](http://www.candy-line.io/proandsv.html#candyiot)には、Ethernetケーブルを直接接続することはできませんので、必ずWi-Fiの環境をご用意ください。

上記を実行すると以下のように表示されます。

一覧のSSIDは、ご利用の環境によって表示される内容は変化します。このSSIDの一覧からお使いのSSIDを数字で選択してください。SSIDを非公開にしている場合は、2を入力するとSSIDの入力指示が画面に現れますので、指示に従って入力してください。

```
Configure Edison: WiFi Connection

Scanning: 1 seconds left  

0 :     Rescan for networks
1 :     Exit WiFi Setup
2 :     Manually input a hidden SSID
3 :     your-ssid-1
4 :     your-ssid-2
5 :     your-ssid-3


Enter 0 to rescan for networks.
Enter 1 to exit.
Enter 2 to input a hidden network SSID.
Enter a number between 3 to 5 to choose one of the listed network SSIDs: 5
```

この例では、5を選択したとして進みます。すると、以下のように選択したSSIDで良いかの確認が尋ねられます。選択したSSIDであれば`y`を、間違った場合は`n`を入力してエンターを押します。

```
Is your-ssid-3 correct? [Y or N]: y
```

この例では、`y`を指定したので、次へ進みます。すると、選択したSSIDのパスワードを入力するように求められますので入力してエンターを押しましょう。

```
Password must be between 8 and 63 characters.
What is the network password?: *************
```

入力すると以下のように設定が行われます。

```
Initiating connection to your-ssid-3. Please wait...
Attempting to enable network access, please check 'wpa_cli status' after a minute to confirm.
Done. Please connect your laptop or PC to the same network as this device and go to http://192.168.1.65 or http://edison.local in your browser.
Warning: SSH is not yet enabled on the wireless interface. To enable SSH access to this device via wireless run configure_edison --password first.
```

この状態では、IPアドレスまたは名前でアクセスすることができます。

---

もし上記のようなメッセージが出なければ、WiFi環境を見直してから、再度`configure_edison --wifi`を実行してみましょう。

---

続いて、SSHを有効にするためにパスワードを設定します。以下のコマンドを実行しましょう。

```
configure_edison --password
```

実行すると以下のようにパスワードの入力を求められます。8文字以上、63文字以下の文字列を入力してください。
```
Configure Edison: Device Password

Enter a new password (leave empty to abort)
This will be used to connect to the access point and login to the device.
Password:       **********
```

確認のため同じものを入力します。

```
Please enter the password again:        **********
First-time root password setup complete. Enabling SSH on WiFi interface.
The device password has been changed.
```

これで、SSHが有効になりました。

続いて、ソフトウェアのインストールを行いましょう。[candy-iot-serviceのインストール方法](インストール方法.md)をご覧ください。

* [インストール方法](インストール方法.md)
* [CANDY REDのインストール方法](CANDY-REDのインストール方法.md)
* [Edisonファームウェア更新方法](Edisonファームウェア更新方法.md)

---
COPYRIGHT © 2016 CANDY LINE, Inc. [CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
