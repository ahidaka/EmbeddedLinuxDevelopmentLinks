# EmbeddedLinuxDevelopmentLinks
Embedded Linux Development Links

## [～i.MX8で学ぶ～ 組み込みLinuxハンズオン・セミナ](https://interface.cqpub.co.jp/linux-hands-on/) 参加者向けリンク集

https://interface.cqpub.co.jp/linux-hands-on/

## ハンズオン

ハンズオンで参照、使用するリンクとコマンド集を示します。

コマンドは必ず行頭に、入力対象のコマンドプロンプトがあるのでご注意ください。

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















■■■■■

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


Maaxboard-8ulp 用ファームウェア (Yocto Linux Full Image)
Maaxboard-8ulp 用ファームウェア (BootLoader u-boot Image)




### ハンズオン環境

- [Tera Term (Ver 5.3)](https://github.com/TeraTermProject/teraterm/releases/tag/v5.3)

  https://github.com/TeraTermProject/teraterm/releases/tag/v5.3

- [ハンズオン環境インストール](https://github.com/ahidaka/InstallingWSLEmbeddedLinux)

  https://github.com/ahidaka/InstallingWSLEmbeddedLinux


- [ハンズオン環境構築](https://github.com/ahidaka/BuildingWSLEmbeddedLinux)

  https://github.com/ahidaka/BuildingWSLEmbeddedLinux

