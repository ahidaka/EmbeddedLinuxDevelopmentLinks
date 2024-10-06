# EmbeddedLinuxDevelopmentLinks
Embedded Linux Development Links

## [～i.MX8で学ぶ～ 組み込みLinuxハンズオン・セミナ](https://interface.cqpub.co.jp/linux-hands-on/) 参加者向けリンク集

**2024年10月7日更新（テキスト修正内容追加）**

https://interface.cqpub.co.jp/linux-hands-on/

この文書のページ： **https://ahidaka.github.io/EmbeddedLinuxDevelopmentLinks/**

ソースコード： https://github.com/ahidaka/EmbeddedLinuxDevelopmentLinks

## テキスト修正

先日は、**～i.MX8で学ぶ～組み込みLinuxハンズオン・セミナ テーマ** ②：Linuxデバイス・ドライバ開発入門 にご参加頂きまして、ありがとうございます。テキストの追加・修正をここの場で公開します。

### 修正追加内容一覧

1. ファームウェア書き込み時のケーブル接続
2. ファームウェア書き込み時の u-bootファイル名
3. レシピファイル作成時の抜けと手順の追加・整理
4. bitbake 再実行時のキャッシュクリア手順

#### ファームウェア書き込み時のケーブル接続

ハンズオン中にお知らせした様に、配布テキスト 6ページ のケーブル接続指示が間違っています。正しくは次の通りです。

1.3.4. ファームウェア書き込み（UUU）実行までは、コンソール用USBケーブル (USB Console)は接続しません。最初は、電源用USBケーブル（USB Power）だけの接続として下さい。

そして 1.3.6. ジャンパ設定(Boot Mode)後は、コンソール用USBケーブル (USB Console)と、電源用USBケーブル（USB Power）の両方を接続して下さい。

#### ファームウェア書き込み時の u-bootファイル名

配布テキスト 5ページほか数か所の、UUUコマンドで書き込む u-boot ファイル名が間違っています。正しくは、u-boot-maaxboard-8ulp.**imx** です。以降のこのリンク集の基準も全て修正しました。

#### レシピファイル作成時の抜けと手順の追加・整理

配布テキスト 22ページ 3.3.1.1. レシピファイルのコピーと編集 に編集内容の抜けがありました。
正しくは本リンク集の該当項目に、追加情報とともに整理して記載しています。

#### bitbake 再実行時のキャッシュクリア手順

前項に関連して、追加レシピの内容や追加ファイルの内容に誤りがあった場合は、再度 bitbake し直してもデータがキャッシュされているため、作成されるイメージが変更されないことを確認しています。

この問題に対応するために、再度 bitbake する際に、古いキャッシュをクリアしてから bitbake を実行する手順を本リンク集の最後に追加して説明しています。

## ハンズオン

ハンズオン中にオンラインで参照、使用するリンクとコマンド集です。

コマンドは必ず行頭に、入力対象のコマンドプロンプトがあるのでご注意ください。

**エディタ** は **nano** **vi/vim** **emacs** が利用出来ます。

### WSL からコマンドプロンプトに戻る

```sh
$ exit
```

### WSLの再起動

```sh
$ sudo shutdown -r now
```

### WSLの終了

```sh
$ sudo shutdown -h now
```
後に以下を実行。

```cmd
> wsl --shutdown
```

## システムの起動

### ツールとファームウェアの入手

- [Tera Term v5.3](https://github.com/TeraTermProject/teraterm/releases/tag/v5.3)

  https://github.com/TeraTermProject/teraterm/releases/tag/v5.3

- [UUU 1.5.21 (Universal Update Utility)](https://github.com/nxp-imx/mfgtools/releases/tag/uuu_1.5.21)
  
  https://github.com/nxp-imx/mfgtools/releases/tag/uuu_1.5.21


- ファームウェア [Yocto Linux Full Image (wic)](https://avtinc.sharepoint.com/:u:/t/ET-Downloads/EX0ZecM2petAnDaj2Ky3d7MByKoB55fRASdztgjpTxtYuw)

  https://avtinc.sharepoint.com/:u:/t/ET-Downloads/EX0ZecM2petAnDaj2Ky3d7MByKoB55fRASdztgjpTxtYuw

- ファームウェア [BootLoader u-boot Image](https://avtinc.sharepoint.com/:u:/t/ET-Downloads/ES_q6BqSIV9JssbRsO5n-2UB2AtMwp3Ygkjp0Viu5iUrow)

  https://avtinc.sharepoint.com/:u:/t/ET-Downloads/ES_q6BqSIV9JssbRsO5n-2UB2AtMwp3Ygkjp0Viu5iUrow

### ファームウェア書き込み (UUU)

電源側USBケーブルだけを接続した状態（コンソールUSBは取り外し）で、コマンドプロンプトを起動して、UUUコマンドでファームウェアを書きこみます。
```cmd
> uuu -b emmc_all u-boot-maaxboard-8ulp.imx avnet-image-full-maaxboard-8ulp.wic
```

#### ssh からのログイン

IPアドレス調査。
```sh
$ ip a
```

### LED制御

sysfs LED ディレクトリ。

```sh
# cd /sys/class/leds
# ls
```

ledblue ディレクトリの中を確認。
```sh
# ls ledblue
```

赤と緑を点灯。
```sh
# echo 0 > /sys/class/leds/ledblue/brightness
# echo 1 > /sys/class/leds/ledgreen/brightness
# echo 1 > /sys/class/leds/ledred/brightness
```

### Maaxboard 電源断

```
# shutdown -h now
```

コンソールの **Power down** メッセージを確認後、電源側USBコネクターを切断して下さい。

## ハンズオン環境

### ドライバ開発で使う

動作環境の構築手順は、**ハンズオン環境構築** 資料として公開しています。
https://github.com/ahidaka/BuildingWSLEmbeddedLinux

### WSL 環境確認

最新版へのシステムの更新と、treeコマンドのインストール確認。

```sh
$ cd
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install tree -y
```

### ディレクトリ構成

```sh
$ ls ~/linux-imx
$ ls ~/toolchain
$ ls ~/toolchain/rm-gnu-toolchain-12.2.rel1-x86_64-aarch64-none-linux-gnu
$ ls ~/imx-yocto-bsp
$ ls ~/imx-yocto-bsp/sources/
$ ls ~/imx-yocto-bsp/maaxboard-8ulp/build/
```

# ドライバ・モジュールの開発

## ダウンロード

WSL上に作業ディレクトリ（以降 work）を作成してダウンロード。

```sh
$ mkdir work; cd work;
$ git clone https://github.com/ahidaka/HelloLinuxDriver.git
$ git clone https://github.com/ahidaka/SysfsLedController.git
$ git clone https://github.com/ahidaka/GeneralIoTModules.git
```

wgetでダウンロード入手。

```sh
$ cd ~/work
$ wget http://www.devdrv.co.jp/download/tse/202409yocto/CROSS_ENV
$ wget http://www.devdrv.co.jp/download/tse/202409yocto/send_udp.ko.xz
```

## 準備用の事前ビルド

```sh
$ cd ~/work
$ source CROSS_ENV
$ cd SysfsLedController/sysfs_led; make
$ cd ~/work/GeneralIoTModules/udp; make
$ cd ~/work; tar xJvf send_udp.ko.xz
```

## AI コーディング

### Greeting ドライバ

####  Windows copilot プロンプトのサンプル

```
こんちは！あなたは優秀なLinuxカーネルに詳しいIoTプログラマーです。
初心者用の学習用に、単純な演習用のLinuxローダブルモジュールを次の条件で作成してください。
1. モジュール名は、greeting.ko とします。
2. ローダブルモジュール用のsysfs パラメータとして"debug" というint型の値、初期値'0'を持ちます。
3. 起動時にprintkで"Greetings! debug=%d" というメッセージで、debug パラメータの値を表示します。
4. Linuxカーネル 6.2 でビルドするためのMakefileも同時に出力します。
```

応答。

**greeting.c**

「実際の画面を参照してください」

**Makefile**

「実際の画面を参照してください」

```
ありがと。試してみます。
```

**ここで、実際にビルドして、ファイル転送後、ロードして動作確認します。**

#### ソースファイルの書き出し（Windows）

```sh
$ cat > greeting.c
```

```sh
$ cat > Makefile
```

#### ソースコード修正とビルド（WSL Tera Term）

この時 Makefileがセルフコンパイル用記述の場合は、カーネルディレクトリ参照定義を **$(KDIR)** に修正します。
またMakefileの字下げ行頭文字が「タブ」である点に十分注意します。

```
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
```
の記述を以下の様に修正。行頭をタブに変更することを忘れずに。
```
    make -C ＄(KDIR) M=$(PWD) modules
```

ビルドします。

```sh
$ make
```

#### Makefileの解説

以下で greeting の全ソースコードを公開しています。

https://github.com/ahidaka/GreetingLinuxDriver

#### モジュール転送（WSL）

Maaxboardに転送。
**192.168.51.154** はMaaxboard のIPアドレスです。実際のアドレスに書き換えます。

```sh
$ scp greeting.ko root@192.168.51.154:
```
または
```
$ rsync -e ssh -a greeting.ko root@192.168.51.154:
```

#### ロード・実行（Maaxboard）

```
# cd
# insmod greeting.ko debug=5
```

#### Windows copolot

ビルド、転送、ロード、動作確認した後のお礼。

```
ありがと。一発で完璧に動きました！すごいです。感激です。
```

ジョーク！
```
エッヘン。すごいだろう！と言って自慢してみてください。
```

## 他のローダブルモジュール

前述の手順でビルドした、次の4種類のカーネルモジュールを使用して、ローダブルモジュールの取り扱いを確認します。HelloLinuxDriver リポジトリのモジュールは元、**インターフェース2005年7月号掲載** のサンプルドライバーが元ですが、Copilotの助けでカーネル6.xに移植しました。

| Use | Repository | Folder | target | 説明 |
| -- | -- | -- | -- | -- |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | hello | hello.ko | デバッグメッセージ |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | hello | hello_m.ko | 複数ソース |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | hello | params.ko | 様々なモジュール・パラメータ |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | schedule | kthread.ko | Kernel Thread |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | schedule | period.ko | 定期実行 Kernel Thread |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | schedule | tasklet.ko | tasklet  |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | schedule | workq.ko | 汎用 Workqueue |
| - | [HelloLinuxDriver](https://github.com/ahidaka/HelloLinuxDriver) | schedule | workq2.ko | カスタム Workqueue |
| Yes | [SysfsLedController](https://github.com/ahidaka/SysfsLedController) | sysfs_led | **sysfs_led_lib.ko** | sysfsLEDライブラリ |
| Yes | [SysfsLedController](https://github.com/ahidaka/SysfsLedController) | sysfs_led | **sysfs_led_test.ko** | sysfsLED実行 |
| Yes | [GeneralIoTModules](https://github.com/ahidaka/GeneralIoTModules) | udp | **send_udp.ko** | UDP汎用ファイル送信 |
| Yes | [GeneralIoTModules](https://github.com/ahidaka/GeneralIoTModules) | udp | **receive_udp.ko** | UDP汎用ファイル受信 |

## sysfs_led

- sysfs_led_lib.ko
- sysfs_led_test.ko

### sysfs_led ハンズオン

#### モジュール転送（WSLで操作）

WSLのコマンドプロンプトで操作して、Maaxboardに転送。
**192.168.51.154** はMaaxboard のIPアドレスです。実際のアドレスに書き換えます。

```sh
$ scp sysfs_led_lib.ko root@192.168.51.154:
$ scp sysfs_led_tesl.ko root@192.168.51.154:
```
または
```
$ rsync -e ssh -a  sysfs_led_lib.ko root@192.168.51.154:
$ rsync -e ssh -a  sysfs_led_tesl.ko root@192.168.51.154:
```

#### ロード（Maaxboard）

```sh
# insmod sysfs_led_lib.ko
# insmod sysfs_led_test.ko
```

#### 実行（Maaxboard）

SYSFSパラメータにパターンを出力して確認。
**テキストファイル中に/sys/modules/...** とあるのは、**/sys/module** の間違いです。

```sh
# echo 1 > /sys/module/sysfs_led_test/parameters/pattern
# echo 2 > /sys/module/sysfs_led_test/parameters/pattern
# echo 3 > /sys/module/sysfs_led_test/parameters/pattern
# echo 4 > /sys/module/sysfs_led_test/parameters/pattern
# echo 7 > /sys/module/sysfs_led_test/parameters/pattern
# echo 0 > /sys/module/sysfs_led_test/parameters/pattern
```

## send_udp/receive_udp

### ハンズオン：送受信とも Maaxboard

#### 送受信ともMaaxboard：モジュール転送（WSL）

WSLのコマンドプロンプトで操作して、モジュールをMaaxboardに転送。
**192.168.51.154** はMaaxboard のIPアドレスです。実際のアドレスに書き換え。
**テキストファイル中にsend_udd.ko** とあるのは、**send_udp.ko** の間違いです。

```sh
$ scp send_udp.ko root@192.168.51.154:
$ scp reseive_udp.ko root@192.168.51.154:
```
または
```
$ rsync -e ssh -a  send_udp.ko root@192.168.51.154:
$ rsync -e ssh -a  reseive_udp.ko root@192.168.51.154:
```

#### 送受信ともMaaxboard：ロード（Maaxboard）

Maaxboardでロード。
```sh
# insmod send_udp.ko debug=1
# insmod receive_udp.ko debug=1
```

#### 送受信とも Maaxboard：実行（Maaxboard）

SYSFSのdataパラメータを使用して、データ送信後、次に受信。
**テキストファイル中に/sys/modules/...** とあるのは、**/sys/module** の間違いです。

```sh
# echo "This is test send data." > /sys/module/send_udp/parameters/data
# cat /sys/module/receive_udp/parameters/data
```
実行時にシリアルコンソールのデバッグログ出力確認。
syslog出力確認。

```sh
# tail /var/log/syslog
```

### ハンズオン：送信はWSL 受信はMaaxboard

#### 送信はWSL 受信は Maaxboard：モジュール転送（WSL）

WSLのコマンドプロンプトで操作して、受信モジュールをMaaxboardに転送。
**192.168.51.154** はMaaxboard のIPアドレスです。実際のアドレスに書き換え。

```sh
$ scp reseive_udp.ko root@192.168.51.154:
```
または
```
$ rsync -e ssh -a  reseive_udp.ko root@192.168.51.154:
```

#### 送信はWSL 受信は Maaxboard：ロード（WSLとMaaxboard）

```sh
$ cd ~/work
$ sudo insmod send_udp.ko debug=1
```

Maaxboardでロード。
```sh
# insmod send_udd.ko debug=1
```

#### 送信はWSL 受信は Maaxboard：実行（WSLとMaaxboard）

SYSFSのdataパラメータを使用して、データを送信後、受信。

**192.168.51.154** はMaaxboard のIPアドレスです。実際のアドレスに書き換え。
```sh
$ sudo echo 192.168.51.154 > /sys/module/send_udp/parameters/ip
$ sudo echo "This is test send data." > /sys/module/send_udp/parameters/data
```

Maaxboard 受信。
```sh
# cat /sys/module/receive_udp/parameters/data
```

シリアルコンソールのデバッグログ出力確認。syslog出力を確認。

```sh
# tail /var/log/syslog
```

# Yocto Project レシピ作成手順のハンズオン

## ビルド環境設定

```sh
$ cd ~/imx-yocto-bsp
$ source sources/poky/oe-init-build-env maaxboard-8ulp/build
```
この、oe-init-build-env の呼び出しで、build ディレクトリに移動します。

## 最初の独自レイヤーを作成・追加する

~/imx-yocto-bsp/maaxboard-8ulp/build$ ディレクトリに移動したことを確認して、最初に meta-greeting レイヤーを作成します。
```sh
$ bitbake-layers create-layer meta-greeting
```

つづいて。
```sh
$ bitbake-layers add-layer meta-greeting
```

tree コマンドで確認。

```sh
$ tree meta-greeting
```

layer.conf の内容確認。

```sh
$ cat meta-greeting/conf/layer.conf
```

example_0.1.bb ファイル確認。
```sh
$ cat meta-greeting/recipes-example/example/example_0.1.bb
```

### レシピを作成する

example レシピを削除。
```sh
$ cd meta-greeting
$ rm -rf recipes-example
```

フォルダ作成。
```sh
$ mkdir -p recipes-greeting/greeting
$ cd recipes-greeting/greeting
$ mkdir files
```

#### レシピファイルのコピーと編集

```sh
$ cp ~/imx-yocto-bsp/sources/poky/meta-skeleton/recipes-kernel/hello-mod/hello-mod_0.1.bb greeting_0.1.bb
```

エディタで編集します。

**テキスト22ページ 3.3.1.1. レシピファイルのコピーと編集** に編集内容の抜けがありましたので、修正掲載します。
以下の部分、最後の **kernel-module-greeting** の行の修正が抜けていました。

```
前略
LICENSE = "MIT"
LIC_FILES_CHKSUM = "file://${COMMON_LICENSE_DIR}/MIT;md5=12f884d2ae1ff87c09e5b7ccc2c4ca7e"

inherit module

SRC_URI = "file://Makefile \
           file://greeting.c \
          "

S = "${WORKDIR}"

# The inherit of module.bbclass will automatically name module packages with
# "kernel-module-" prefix as required by the oe-core build environment.

RPROVIDES:${PN} += "kernel-module-greeting"
```

#### 参考：greeting.c ソースをGitHubから取得する場合

以下の clone コマンドで取得します。Copilotで作成して動作確認済の場合は不要です。

```sh
$ cd
$ git clone https://github.com/ahidaka/GreetingLinuxDriver.git
```
cp コマンドで greeting.c ソースコードだけをコピーします。

```sh
cd ~/imx-yocto-bsp/maaxboard-8ulp/build
$ cp ~/GreetingLinuxDriver/greeting/greeting.c meta-greeting/recipes-greeting/greeting/files
```

#### Makefile のコピーと編集

Makefileファイルをコピー、先頭行のターゲット名だけを変更して利用。
```sh
$ cp ~/imx-yocto-bsp/sources/poky/meta-skeleton/recipes-kernel/hello-mod/files/Makefile meta-greeting/recipes-greeting/greeting/files
```

修正前のMakefileの1行目
```
obj-m := hello.o
```

修正後のMakefileの1行目
```
obj-m := greeting.o
```

### レイヤー追加の記述

#### local.conf の修正

local.conf 編集。

```
...前略...
CONF_VERSION = "2"

IMAGE_INSTALL:append = " greeting"
...後略...
```

### 単一レシピだけのbitbake

```sh
bitbake greeting
```

エラー発生。
```
 md5 checksum is 0835ade698e0bcf8506ecda2f7b4f302
```
 「checksum is 」 で指摘の値をコピーして書き換え。

```sh
$ bitbake greeting
```

bitbake 出力の、デバッグシンボル付きのローダブルモジュールの場所

```
./work/maaxboard_8ulp-poky-linux/greeting/0.1-r0/greeting.ko
```

シンボル削除済のローダブルモジュールの場所
```
./sysroots-components/maaxboard_8ulp/greeting/lib/modules/6.1.22+g78ce688d5a79/extra/greeting.ko
```

### 動作確認

#### core-image-minimal 作成

**core-image-minimal** は、最小構成でビルドするために poky で指定されている包括的なレシピです。

```sh
$ bitbake core-image-minimal
```

作成される転送用のROMイメージ。
```
~/imx-yocto-bsp/maaxboard-8ulp/build/tmp/deploy/images/maaxboard-8ulp/core-image-minimal-maaxboard-8ulp.wic
```

#### core-image-minimal 動作確認

■ Maaxboard 電源断

```sh
# shutdown -h now
```

■ ファームウェア・コピー

```sh
cp ~/imx-yocto-bsp/maaxboard-8ulp/build/tmp/deploy/images/maaxboard-8ulp/core-image-minimal-maaxboard-8ulp.wic /mnt/c/FIRM
```

■ ファームウェア書き込み

電源切断後、ジャンパピンを設定し直して、**USB電源ケーブルだけの接続** としてMaaxboard の電源を入れてファームウェアをMaaxboard に書き込みます。

```cmd
> uuu -b emmc_all u-boot-maaxboard-8ulp.imx avnet-image-full-maaxboard-8ulp.wic
```

■ 動作確認

Maaxboard にファームウェア書き込み完了後は、ジャンパピンを設定し直して、USB電源ケーブルだけとシリアルコンソールケーブルの両方を接続して電源を入れて、動作確認します。

ハンズオン時間の都合上、小規模ルートファルシステムの core-image-minimal レシピで bitbake したため、Maaxboard では sshdが動作しない点に注意してください。

```sh
# depmod -a
# modprove greeting
```

シリアルコンソールで、以下のメッセージ出力を確認します。

```
greeting: loading out-of-tree module taints kernel.
Greetings! debug=0
```

greeting.ko は次の場所にインストールされています。

```
/lib/modules/6.1.22+g78ce688d5a79/extra/greeting.ko
```


### 追加の課題

時間がある方は、同様に追加するレシピ名を receive-udp として、meta-receive-udp を作成、追加して動作確認します。

```sh
$ bitbake-layers create-layer meta-receive-udp
$ bitbake-layers add-layer meta-receive-udp
```
bitbake コマンド。

```sh
$ bitbake core-image-minimal
```

### bitbake 再実行時のキャッシュクリア

追加レシピの内容や追加ファイルの内容に誤りがあった場合は、再度 bitbake し直してもデータがキャッシュされているため、作成されるイメージが変更されません。この問題に対応するために、再度 bitbake する際に、古いキャッシュをクリアする方法を説明します。

キャッシュクリアは、bitbake 対象の該当レシピの最小のもので実行します。例えば今回のハンズオンで、bitbake core-image-minimal を再度実行する場合でも、その前に動作確認として実行した、テキスト23ページ 3.3.3. 単一レシピだけのbitbakeからやり直します。その際にキャッシュをクリアするための

```sh
$ bitbake -c cleansstate greeting
```
と **-c cleansstate** オプションを付けて bitbake を実行します。

core-image-minimal を再実行する場合は、続いて、

```sh
$ bitbake core-image-minimal
```

レシピの内容やレシピに含まれるファイルを修正、変更した場合は、この様にして何回でもレシピの内容を修正しながら、bitbake を試すことが可能です。

### 参考資料

- [GitHub MaaXBoard-8ULP-HUB](https://github.com/Avnet/MaaXBoard-8ULP-HUB)

  https://github.com/Avnet/MaaXBoard-8ULP-HUB

- [Yocto-UserManual-V3.1](https://www.avnet.com/wps/wcm/connect/onesite/07e9ad99-8969-40c1-b632-db97adf350d0/MaaXBoard-8ULP-Linux-Yocto-UserManual-V3.1.pdf?MOD=AJPERES)

  https://www.avnet.com/wps/wcm/connect/onesite/07e9ad99-8969-40c1-b632-db97adf350d0/MaaXBoard-8ULP-Linux-Yocto-UserManual-V3.1.pdf?MOD=AJPERES

- [Yocto-Development-Guide-V3.1](https://www.avnet.com/wps/wcm/connect/onesite/4fa62a19-239c-40c9-aff6-8a122f993f1e/MaaXBoard-8ULP-Linux-Yocto-Development-Guide-V3.1.pdf?MOD=AJPERES)

  https://www.avnet.com/wps/wcm/connect/onesite/4fa62a19-239c-40c9-aff6-8a122f993f1e/MaaXBoard-8ULP-Linux-Yocto-Development-Guide-V3.1.pdf?MOD=AJPERES

- [Hardware Guides v1.0](https://www.avnet.com/wps/wcm/connect/onesite/60e2bb73-e479-4f76-821f-0b811ae52643/MaaXBoard-8ULP-User-Guide-v1.0.pdf?MOD=AJPERES)

  https://www.avnet.com/wps/wcm/connect/onesite/60e2bb73-e479-4f76-821f-0b811ae52643/MaaXBoard-8ULP-User-Guide-v1.0.pdf?MOD=AJPERES

- uuu (Universal Update Utility), mfgtools 3.0(https://github.com/nxp-imx/mfgtools)

  https://github.com/nxp-imx/mfgtools

### ハンズオン環境

- [ハンズオン環境インストール](https://github.com/ahidaka/InstallingWSLEmbeddedLinux)

  https://github.com/ahidaka/InstallingWSLEmbeddedLinux


- [ハンズオン環境構築](https://github.com/ahidaka/BuildingWSLEmbeddedLinux)

  https://github.com/ahidaka/BuildingWSLEmbeddedLinux
