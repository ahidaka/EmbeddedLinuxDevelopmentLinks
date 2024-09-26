# EmbeddedLinuxDevelopmentLinks
Embedded Linux Development Links

## [～i.MX8で学ぶ～ 組み込みLinuxハンズオン・セミナ](https://interface.cqpub.co.jp/linux-hands-on/) 参加者向けリンク集

https://interface.cqpub.co.jp/linux-hands-on/

この文書のページ： **https://ahidaka.github.io/EmbeddedLinuxDevelopmentLinks/**

ソースコード： https://github.com/ahidaka/EmbeddedLinuxDevelopmentLinks

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

コマンドプロンプトを起動して、UUUコマンドでファームウェアを書きこみます。
```cmd
> uuu -b emmc_all u-boot-maaxboard-8ulp.bin avnet-image-full-maaxboard-8ulp.wic
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

エディタで編集。

```
前略
LICENSE = "MIT"
LIC_FILES_CHKSUM = "file://${COMMON_LICENSE_DIR}/MIT;md5=12f884d2ae1ff87c09e5b7ccc2c4ca7e"

inherit module

SRC_URI = "file://Makefile \
           file://greeting.c \
          "
後略
```

greeting.c ソースコードを取得の場合。

```sh
$ cd
$ git clone https://github.com/ahidaka/GreetingLinuxDriver.git
```

greetingLinuxDriver のリポジトリ：https://github.com/ahidaka/GreetingLinuxDriver

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

Maaxboard の電源を入れてファームウェアをMaaxboard に書き込み。

```cmd
> uuu -b emmc_all u-boot-maaxboard-8ulp.bin avnet-image-full-maaxboard-8ulp.wic
```

■ 同様確認

```sh
# depmod -a
# modprove greeting
```

### 

追加するレシピ名は receive-udp として、meta-receive-udp を作成、追加。

```sh
$ bitbake-layers create-layer meta-receive-udp
$ bitbake-layers add-layer meta-receive-udp
```
ビルドコマンド。

```sh
$ bitbake core-image-minimal
```

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
