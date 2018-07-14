----------------------------------------------
Getting start for RX65N Amazon FreeRTOS
----------------------------------------------
Thank you for interesting about RX65N and Amazon FreeRTOS.
This guide is for your environment setup and confirm demos behavior.

SheltyDog@Renesas writes this guide and has responsibility of this project.
If you have any question/suggestion/opinion, please visit following page and post it.
https://github.com/NoMaY-jp/amazon-freertos-renesas-rx

Now Amazon provides great real time OS with network software for
MCU (like some peripheral with 100MHz class CPU) as "Amazon FreeRTOS".
As you know "Amazon Web Service(AWS)" is one of biggest IoT Cloud Service in W/W.
"Amazon FreeRTOS" can make a way to connect the "Amazon Web Service" like following steps.

Download or Clone repository from GitHub.
The download zip file name is "amazon-freertos-master.zip".
Extract this zip or your clone directory has "demos" and "lib" directory readme, etc.
This is our root directory called <root>.

Getting start steps:
 step1:  Refer to the Development Environment (recommended) section to get the board and tools.
 step2:  Setup tools for your PC.
 step3:  Download RX65N Amazon FreeRTOS from GitHub. (Maybe you already done)
         https://github.com/NoMaY-jp/amazon-freertos-renesas-rx
 step4:  Make your AWS account, and make your "Things" on AWS,
         and enable Security Policy to allow all your device will connect to your "Things".
 step5:  Make your device certification and private key and settings put this into your source code.
         <root>/demos/common/include
          aws_clientcredential.h
           clientcredentialMQTT_BROKER_ENDPOINT[]
           clientcredentialIOT_THING_NAME
          aws_clientcredential_keys.h
           clientcredentialCLIENT_CERTIFICATE_PEM[]
           clientcredentialCLIENT_PRIVATE_KEY_PEM[]
 step6:  Start Renesas IDE (e2 studio) and import Amazon FreeRTOS project.
         import sequence: file->import->existing project into workspace -> select a root directory
         The project folder is placed into <root>/demos/renesas/rx65n-rsk/ccrx-e2studio6
         Please specify this directory only.
 step7:  Get/Put Device Driver from Renesas Webpage and put it into your project.
         Refer to following text.
         <root>/demos/renesas/rx65n-rsk/ccrx-e2studio6/src/realtime_OS_pkg/get!.txt
 step8:  Configure your environment using Smart Configurator.
         Please double click aws_demos.scfg on your Project Explorer on e2 studio.
         You can start Smart Configurator with already configured value.
         You can confirm following modules are installed on your Component Tab. (But not generated the code)
         - r_bsp
         - r_sci_rx
         - r_cmt_rx
         - r_flash_rx
         - r_ether_rx
         - r_byteq
         After confirmation, please click the generate button on Smart Configurator.
         The device drivers code you confirmed are generated into following directory,
         and some settings (include path, section, link the library, etc) will be applied.
         <root>/demos/renesas/rx65n-rsk/ccrx-e2studio6/src/smc_gen/
         ** notice **
         No need to change your device setting from R5F565NEHxFB to R5F565NEDxFB on your Board Tab.
 step9:  Build
 step10: Execute, confirm console log will show the Echo message from AWS.
         The log will be output from G1CUSB connector as UART/USB.
         Please set baud-rate as 115200bps, 8bit-data, no-parity, 1 stop-bit,
         and "LF" only as return code for your console.
  
Thanks for Amazon team provides great software as Open Source and great IoT Cloud Service.
And Thanks for NoMaY-san provides many many useful information to port the Amazon FreeRTOS to RX65N,
and manages GitHub repository for this project.
And Thanks for Renesas RX MCUs business unit member funds for me,
and helps some hardware/software development.
I hope this solution will be helpful for embedded system developer in W/W.

--------------------------------------------------------------------------
Change Logs
--------------------------------------------------------------------------
v0.0.6:
[ADDED] Support RX65N GR-ROSE.
[ADDED] Compiler pre-processor macro "__RX" to fix e2 studio local issue for pre-build code analysis.
[ADDED] Settings for indexer e2 studio local issue for pre-build code analysis.
        - e2 studio project for each of the board, RX65N RSK, RX65N Envision Kit, RX65N GR-ROSE.
[UPDATED] prvMiscInitialization() call timing to avoid the system bus error comes from corrupting printf() output.
[UPDATED] MAC address from temporary MAC address to renesas sample code MAC address.
[UPDATED] e2 studio version from v620 to v630.
[UPDATED] RX Driver Package version from v113 to v114.

v0.0.5:
[UPDATED] Follow the upstream from Amazon FreeRTOS v1.2.7.
[UPDATED] Readme text step8 for additional notice.

v0.0.4:
[UPDATED] Readme text encode from SJIS to UTF8.
[UPDATED] Readme text step8 for more details.

v0.0.3:
[UPDATED] Follow the upstream from Amazon FreeRTOS v1.2.6.

v0.0.2:
[UPDATED] Follow the upstream from Amazon FreeRTOS v1.2.5.
[REMOVED] Getting start step7 from #ifdef 0 to 1.
[UPDATED] Clarify Getting start root directory path same as download zip "amazon-freertos-master".

v0.0.1: released
[ADDED] RX65N supports Amazon FreeRTOS Release Version 1.2.3 in tentative.
        Only confirmed Echo demo using Ethernet.

--------------------------------------------------------------------------
Development Environment (recommended)
--------------------------------------------------------------------------
Board: Renesas Starter Kit+ for RX65N-2MB
    [en] https://www.renesas.com/en-us/products/software-tools/boards-and-kits/renesas-starter-kits/renesas-starter-kitplus-for-rx65n-2mb.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/boards-and-kits/renesas-starter-kits/renesas-starter-kitplus-for-rx65n-2mb.html

Compiler: CC-RX V2.08 (you need non-expired evaluation license or product license to build Amazon FreeRTOS)
    [en] https://www.renesas.com/en-us/products/software-tools/tools/compiler-assembler/compiler-package-for-rx-family-e2studio.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/tools/compiler-assembler/compiler-package-for-rx-family-e2studio.html

IDE: e2 studio V6.3.0
    [en] https://www.renesas.com/en-us/products/software-tools/tools/ide/e2studio.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/tools/ide/e2studio.html
    
Debugger: E1 Emulator (no need to buy because Renesas Starter Kit has this one into package)
    [en] https://www.renesas.com/en-us/products/software-tools/tools/emulator/e1.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/tools/emulator/e1.html

Device Driver: RX Driver Package v114
    [en] https://www.renesas.com/en-us/products/software-tools/software-os-middleware-driver/software-package/rx-driver-package.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/software-os-middleware-driver/software-package/rx-driver-package.html

Special Device Driver for FreeRTOS:
    [en] https://www.renesas.com/en-us/products/software-tools/software-os-middleware-driver/software-package/rx-real-time-os-package.html
    [ja] none
    
Comment:
 Renesas Starter Kit+ for RX65N-2MB is expensive/huge spec for just prototyping phase.
 I am preparing low-priced/small-spec kit as expansion board for "Target Board for RX Family".
    [en] https://www.renesas.com/en-us/products/software-tools/boards-and-kits/cpu-mpu-boards/rx-family-target-board.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/boards-and-kits/cpu-mpu-boards/rx-family-target-board.html
 Current developments is using Ethernet but I will move this to WiFi.
 And I am also preparing to corresponds to GCC for release from CC-RX compiler limitation.
 
--------------------------------------------------------------------------
Development Environment (optional)
--------------------------------------------------------------------------
Board: RX65N Envision Kit
    [en] https://www.renesas.com/en-us/products/software-tools/boards-and-kits/renesas-promotion-boards/rx65n-envision-kit.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/boards-and-kits/renesas-promotion-boards/rx65n-envision-kit.html

         The log will be output from CN14(PMOD:1-6pin) connector as PMOD UART/USB.
         Please set baud-rate as 115200bps, 8bit-data, no-parity, 1 stop-bit,
         and "LF" only as return code for your console.
         PMOD UART/USB convertor is provided by Digilent.
         https://store.digilentinc.com/pmod-usbuart-usb-to-uart-interface/

         Comment:
           RX65N Envision Kit has no parts related Ethernet.
           Please implements LAN8720A and RJ45 connector onto your RX65N Envision Kit.

Board: RX65N GR-ROSE proto1
    [en] now preparing
    [ja] now preparing
         [event info] http://gadget.renesas.com/ja/event/2018/RenesasNight13.html

         The log will be output from CN9 10pin=TxD12(PE1) connector as UART.
         Please set baud-rate as 115200bps, 8bit-data, no-parity, 1 stop-bit,
         and "LF" only as return code for your console.
         PMOD UART/USB convertor can be used for this signal.
         https://store.digilentinc.com/pmod-usbuart-usb-to-uart-interface/

         Please contact as following.
         PMOD UART/USB ----- RX65N GR-ROSE CN9
         1             -----
         2             ----- 10pin
         3             -----
         4             -----
         5             ----- 5pin
         6             ----- 6pin

         This pin assign is wrong. We will fix this after proto2.

         [How to connect E1 Emulator]
         GR-ROSE CN2-TH 4pins are connected to RX65N Debug Interface called FINE.
         You can connect E1 or E2 Emulator to this pins as following.
         GR-ROSE CN2-TH ----- Emulator 14pin connector
         pin1(VCC)      ----- pin8
         pin2(GND)      ----- pin2, pin12, pin14
         pin3(MD)       ----- pin7
         pin4(#RES)     ----- pin13

         Workaround for circuit bug:
           You have to connect ESP-WROOM-02D pin4 to GND (CN1 pin1)
           before connecting debugger from IDE operation (e2 studio has "BUG" icon for start debugging).
           And, you have to release ESP-WROOM-02D pin4 from GND after connecting.
           You can see pin1 on left-upper corner nearby "E" character on "ESPRESSIF" logo.
           Pin4 is lower 4pins from pin1.

IDE: CS+
    [en] https://www.renesas.com/en-us/products/software-tools/tools/ide/csplus.html
    [ja] https://www.renesas.com/ja-jp/products/software-tools/tools/ide/csplus.html

--------------------------------------------------------------------------
Connection Pattern
--------------------------------------------------------------------------
  pattern1:
  osi	protocol	implemented into
  7	aws		Amazon FreeRTOS
  7	mqtt		Amazon FreeRTOS
  6	ssl/tls		wifi module
  5	socket		wifi module
  4	tcp		wifi module
  3	ip		wifi module
  2	ether		wifi module
  1	phy		wifi module

  RX65N Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
  RX231 Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
  RX130 Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
  RX65N Target Board + Cloud Option Board (with Espressif ESP8266)
  RX231 Target Board + Cloud Option Board (with Espressif ESP8266)
  RX130 Target Board + Cloud Option Board (with Espressif ESP8266)
  RX65N GR-ROSE (with Espressif ESP8266)

  pattern2:
  osi	protocol	implemented into
  7	aws		Amazon FreeRTOS
  7	mqtt		Amazon FreeRTOS
  6	ssl/tls		Amazon FreeRTOS
  5	socket		Amazon FreeRTOS
  4	tcp		Amazon FreeRTOS
  3	ip		Amazon FreeRTOS
  2	ether		Amazon FreeRTOS(RX Ether specific)
  1	phy		ether-phy

  RX65N RSK <first step>
  RX65N Envision Kit <first step>
  RX65N GR-ROSE
  RXxxN Envision Kit (Murata Type 1FX on board)
  
  pattern3:
  osi	protocol	implemented into
  7	aws		Amazon FreeRTOS
  7	mqtt		Amazon FreeRTOS
  6	ssl/tls		Amazon FreeRTOS
  5	socket		Amazon FreeRTOS
  4	tcp		Amazon FreeRTOS
  3	ip		Amazon FreeRTOS
  2	ether		Amazon FreeRTOS(RX SDIO-wifi specific)
  1	phy		wifi radio

  RX65N RSK + SDIO wifi SDK (with Murata Type 1FX)
  RX65N Envision Kit + SDIO wifi SDK (with Murata Type 1FX)
  RXxxN Envision Kit (Murata Type 1FX on board)
  
--------------------------------------------------------------------------
Development Environment (tested or no matrix)
--------------------------------------------------------------------------

Borad number:
 (1)Renesas Starter Kit+ for RX65N-2MB
 (2)RX65N Envision Kit
 (3)RX65N GR-ROSE proto1

IDE number:
 (1)e2 studio
 (2)CS+
 (3)IAR

Compiler number:
 (1)CC-RX
 (2)GCC
 (3)IAR

v0.0.6:
         IDE      (1)         (2)         (3)
         Compiler (1) (2) (3) (1) (2) (3) (1) (2) (3)
Board (1)          x           x                     
      (2)          x           x          N/A N/A    
      (3)          x                      N/A N/A    

--------------------------------------------------------------------------
RX65N Device Introduction
--------------------------------------------------------------------------
RX65N is powerful device for IoT embedded system.
RX65N has some useful peripheral for getting sensor data, control some motors,
and communication with some devices using USB/Ether/SD card/SDIO/UART/I2C/SPI/etc,
and original security IP can make "Root of Trust" as device security,
and LCD controller that can connect to generic LCD
(recommended 480x272 resolution with double buffer (256x2KB)),
with huge internal memory (max ROM=2MB, RAM=640KB)
with powerful/low current consumption (34 CoreMark/mA),
Renesas original CPU(RXv2 core)@120MHz using 40nm process.
https://www.renesas.com/en-us/about/press-center/news/2017/news20171113.html

--------------------------------------------------------------------------
EOF
--------------------------------------------------------------------------
Following text is SheltyDog memo written in Japanese.
Please ignore this in basically.

----------------------------------------------
Amazon FreeRTOS ポーティング記録
----------------------------------------------
■背景
ルネサス公式コミュニティ「かふぇルネ」でAmazon FreeRTOS関連の
話題があり、NoMaY氏がまとめてくれた情報を元にRX65Nで
Amazon FreeRTOSを動作させることを目指す。
https://japan.renesasrulz.com/cafe_rene/f/forum21/4772/amazon-freertos-rx/

本記録は「かふぇルネ」で活動するシェルティが記す。

--------------------------------------------------------------------------
■進捗
--------------------------------------------------------------------------
RX65N Envision Kit、RX65N RSK(2MB版/暗号器あり品)をターゲットにコードメンテを維持します。
下記 Amazon FreeRTOS 1.2.x は適宜最新コードに更新していきます。
2018/04/30時点での適用コードは 1.2.3 です。

①ルネサスTCP/IPをターゲットで動作させる（Etherの動作確認）
②SDIO無線LANを動作確認した時期のFreeRTOS 8.2.2をターゲットで動作させる
③ルネサスのFreeRTOSパッケージ、9.0.0をターゲットで動作させる
④Amazon FreeRTOS 1.2.xのFreeRTOS部分をターゲットで動作させる
⑤Amazon FreeRTOS 1.2.xのFreeRTOS+TCP部分をターゲットで動作させる
⑥Amazon FreeRTOS 1.2.xのmbed TLS部分をターゲットで動作させる
⑦Amazon FreeRTOS 1.2.xのMQTT部分をターゲットで動作させる（AWSへの接続実験）
⑧Amazon FreeRTOS 1.2.xのFreeRTOS+TCP部分のネットワーク層の結合部分を工夫して、
　(1)Ether、(2)SPI接続無線LANモジュール、(3)SDIO無線LANモジュールの3種類を
　切り替えられるようにする　★一旦停止、後ほど(2)に絞って再開
⑨Amazon FreeRTOS 1.2.xのmbed TLS部分の暗号処理プリミティブの
　ソフトウェア実装（AESとかRSAとか）をRX65N内蔵暗号器を使った
　ハードウェア実装に置き換える　★一旦停止
⑩Ether層のゼロコピーに対応する　★一旦停止
⑪Amazon FreeRTOS本家環境にマージし、Amazon FreeRTOS本家コードへの追従を簡単にできるようにする　★いまここ＠シェルティ
⑫Amazon FreeRTOS のGitのforkに登録する
⑬Amazon FreeRTOS のCertificationを受験し合格しGitの本家に登録する
　https://docs.aws.amazon.com/freertos/latest/userguide/freertos-qualification-program.html

--------------------------------------------------------------------------
■課題まとめ★
--------------------------------------------------------------------------
　2018/06/10
　　スマートコンフィグレータのデバイス設定(暗号有品のRX65N)と
　　プロジェクトのデバイス設定(暗号無品のRX65N)とで食い違っていて、
　　スマートコンフィグレータ上で警告が出ている。
　　
　2018/05/01
　　2018/05/01のポーティング記録参照
　
　2018/03/17
　　2018/03/17のポーティング記録参照
　　
　2018/03/03以前
　　NetworkInterface.c 
　　(2)ゼロコピーの概念を無視するが...★
　　(4)(送信側のゼロコピーの仕組みが不明。これもまた後で調べる★)
　　(5)LANケーブル挿抜のイベントをTCP/IP側に通知する仕組みがあるが...★

　　その他
　　・システムログをSCIから出力するようにコード追加すればよい。(★後でメンテ)⇒完了。
　　・コンパイル前処理の構文解析でエラーになっている感じ。→★ツール開発部門に問い合わせてみる。

　その他
　　NoMaY氏の提案の調整。2018/3/11 0:00 のポスト参照。
　　https://japan.renesasrulz.com/cafe_rene/f/forum21/4772/amazon-freertos-rx/27511#27511

--------------------------------------------------------------------------
■ポーティング記録	★印が解決すべき課題
--------------------------------------------------------------------------
2018/07/14
　しばらくぶりの更新。この1か月は内部調整に奔走。この開発は、とても楽しい。
　出張ラッシュがひと段落しての3連休。NoMaY氏がGCC対応のプロジェクトファイルを
　コミットしてくれている。これを試したい。
　その前に、GR-ROSEへのAmazon FreeRTOS移植を実施する。
　
　GR-ROSEとは、がじぇっとるねさすプロジェクトの最新ボード。RX65N搭載。
　ロボットの制御基板をターゲットとした小型ボードであり、通信制御、
　リアルタイム制御用にAmazon FreeRTOSを標準搭載することにした。
　http://gadget.renesas.com/ja/event/2018/RenesasNight13.html
　
　OS/ドライバ周りのインテグレートをシェルティが担当。
　ネットワーク層の上位にROSと呼ばれるロボット制御プロトコルを搭載。
　ROSはAIBOにも載っているソフトウェアとのこと。
　
　RX65N Envision Kitのe2 studio用プロジェクトのファイルをコピーして作業開始。
　リンクフォルダの設定等を調整していく。
　あとはスマートコンフィグレータでEther周り、UART周りの端子を調整。

　Ether周りは特に問題なし。
　あっさりとGR-ROSEでAmazon Web Serviceに繋ぐことができた。
　
　UARTはPMODコネクタに出ているが、PMODのpin7とpin8にSCI-ch1のRxD1、TxD1、
　PMODのpin9とpin10にSCI-ch12のRxD12、TxD12が配線されている。
　PMODのUART仕様はpin3がRxD(PMOD側が入力)、pin4がTxD(PMOD側が出力)であり、
　回路構成と合致しない。
　このPMODはSPI用途なので間違ってはいないが、Amazon FreeRTOSにはUART入出力も必要である。
　(システムログ出力や、アカウントデータのインストールのため等)
　
　RX65N側のUSBのCommunication Device ClassでPC側と通信する手も有るが、
　ファームウェアにUSBドライバが必須になり得策ではない。
　他のプロモーションボードでも同様に基本ファームウェア構成は限りなくシンプルに抑える方針であり、
　システムログ出力はUSBではなく、SCIのUARTで行う。
　
　したがって、GR-ROSE proto1のPMODの配線を修正しUARTを使えるようにする。
　RX65Nのピンマルチをうまくつかえば、ソフトウェアの切り替えでSPIとUARTが同一配線で実現可能。
　現在RSPI1がPMODに配線されているが、残念ながらRSPIの送受信端子はSCIとピン互換ではない。
　PMODに配線するSPIはSCIのSPIモードで妥協し、SCI-ch12のSPI端子4本(UART端子込)を
　PMODのpin1-6に配線することにする。ついでにI2CバスのPMODモジュールも使えるようになる。
　
　まとめると以下。
　
　現状PMOD配線：
　　RSPI-ch1(SPI)  ---> PMOD pin1-4 (fit to PMOD spec)
　　SCI-ch1(UART)  ---> PMOD pin7-8 (not fit to PMOD spec)
　　SCI-ch12(I2C)  ---> PMOD pin9-10 (not fit to PMOD spec)
　次版PMOD配線：
　　SCI-ch12(SPI(SS/MOSI/MISO/SCK))  ---> PMOD pin1-4 (fit to PMOD spec)
　　SCI-ch12(UART(RxD/TxD))          ---> PMOD pin3-4 (fit to PMOD spec)
　　SCI-ch12(I2C(SCL/SDA))           ---> PMOD pin3-4 (not fit to PMOD spec)
　
　ひとまずここでGitHubへのコミット作業。
　
2018/06/10
　特に進捗はしなかった。
　NoMaY氏がコードのメンテを進め、本家v127へ追従してくれている。
　動作確認してv005としてコミットする。
　そろそろSilexモジュールの動作確認も進めなくてはいけない。
　6/8-6/10の3連休もメール処理で終わってしまいそうである。
　何とかしなくては。

2018/06/03
　特に進捗はしなかった。
　Readmeを少し書き換えてv004としてコミットする。
　
2018/05/27
　特に進捗はしなかった。
　NoMaY氏がコードのメンテを進め、本家v126へ追従してくれている。
　動作確認してv003としてコミットする。
　
　開発進捗としては、以下課題が挙がり、対応方法を考えた。
　
　[課題]
　Silex側のTCP/IP機能を使わず、マイコン側でTCP/IPを実装した方式にしたかったが
　Silex側のTCP/IP機能を使わないオプションが無い様子。
　作戦は考えたが、出張週間がまだ続くため検討の時間がない。
　出張が続くとメールが溜まりコードの整備が進まない。
　出張がひと段落した後、6/8-6/10の間が3連休なのでここでどうにかしたい。
　
　[対応方法]
　以下構成とする。これはこれでRX130、RX231、RX65Nで無線LAN実現方法として
　全部共通構造になるので良い。これをpattern1とする。
　有線LANを使うpattern2、SDIO無線LANを使うpattern3もまとめた。
　ボード発売に合わせるのは<first step>と書いたものとする。
　
　pattern1:
　osi	protocol	implemented into
　7	aws		Amazon FreeRTOS
　7	mqtt		Amazon FreeRTOS
　6	ssl/tls		wifi module
　5	socket		wifi module
　4	tcp		wifi module
　3	ip		wifi module
　2	ether		wifi module
　1	phy		wifi module
　
　RX65N Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
　RX231 Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
　RX130 Target Board + Cloud Option Board (with Silex SX-ULPGN)	<first step>
　RX65N Target Board + Cloud Option Board (with Espressif ESP8266)
　RX231 Target Board + Cloud Option Board (with Espressif ESP8266)
　RX130 Target Board + Cloud Option Board (with Espressif ESP8266)

　pattern2:
　osi	protocol	implemented into
　7	aws		Amazon FreeRTOS
　7	mqtt		Amazon FreeRTOS
　6	ssl/tls		Amazon FreeRTOS
　5	socket		Amazon FreeRTOS
　4	tcp		Amazon FreeRTOS
　3	ip		Amazon FreeRTOS
　2	ether		Amazon FreeRTOS(RX Ether specific)
　1	phy		ether-phy

　RX65N RSK <first step>
　RX65N Envision Kit <first step>
　
　pattern3:
　osi	protocol	implemented into
　7	aws		Amazon FreeRTOS
　7	mqtt		Amazon FreeRTOS
　6	ssl/tls		Amazon FreeRTOS
　5	socket		Amazon FreeRTOS
　4	tcp		Amazon FreeRTOS
　3	ip		Amazon FreeRTOS
　2	ether		Amazon FreeRTOS(RX SDIO-wifi specific)
　1	phy		wifi radio

　RX65N RSK + SDIO wifi SDK (with Murata Type 1FX)

2018/05/20
　この1週間で収集したフィードバックは以下3点。
　　ルネサスアメリカ：
　　　①readme.txt の step6-7 でプロジェクトをどのようにインポートするのか
　　　　明確ではない。import->existing project into workspace -> select a root directory
　　　　のように書いたほうがいい。
　　　　 ⇒(シェルティ): OK
　　　②generate!.txt がない
　　　　 ⇒(シェルティ): ある。smc_gen内はコード生成すると関係ないファイルが消える仕様。
　　　　 　　　　　　　　GitHub上には存在するから問題なし。
　　　③一度に一個の環境しかインポートできない旨を書いたほうがいい
　　　　(RSKとEnvision Kitのプロジェクト名が同じだから、
　　　　　同時にインポートしようとするとインポート時にエラーが出る）
　　　　 ⇒(シェルティ): OK
　　ルネサスシンガポール：
　　　./realtime_OS_pkg/r_bsp_rtos/mcu/rx65n/mcu_interrupts.c 
　　　Line851 from #if 0 to #if 1. にあるグループ割り込みの定義は
　　　ユーザアプリ側に移動。Getting startの説明としては不要として良い。
　　　　 ⇒(シェルティ): OK。ただし移動した真意を確かめる必要あり。
　　NoMaY氏：
　　　公式がV1.2.5にアップデート。（2018/05/20 16:00 時点でV1.2.6になったようだ）
　　　RX65N用のフォークをV1.2.5にアップした。その他調整は以下URL参照。
　　　http://japan.renesasrulz.com/cafe_rene/f/forum21/4772/amazon-freertos-rx/28287#28287
　　　　 ⇒(シェルティ): OK
　　　
　作業開始。
　　まず何も考えずリモートフェッチでNoMaY氏の状態を取得。
　　RX65N RSKのe2 studioのプロジェクトで動作確認開始。
　　デバッガの設定で読み込むバイナリ名称とプロジェクト名がおかしかったので修正。
　　　rx65n_rsk_aws -> aws_demos
　　もともとシェルティが作ったときは rx65n_rsk_aws というプロジェクト名だったが
　　NoMaY氏の環境ではaws_demos となっている。落ち着いたらプロジェクト名を調整したい。
　　その後、ルネサスシンガポールのフィードバックを反映。mcu_interrupts.cの
　　グループ割り込みのコードは freertos_usr_func.c に移動。この対処方法はやっぱり
　　何か気になる。元のままでいいのではという気がする。確認する。★
　　step7 のifdefに関する指示を削除した。
　　動作確認。エコー動作OK。
　　なんかAWS接続時にかかる時間が短くなった気がする。

　　RX65N RSKのCS+のプロジェクトで動作確認開始。
　　こちらも特に問題なし。
　　RX65N Envision Kitのe2 studioのプロジェクトで動作確認開始。
　　こちらも特に問題なし。
　　RX65N Envision KitのCS+のプロジェクトで動作確認開始。
　　こちらも特に問題なし。

　ひとまずここまででコミット。v0.02とする。
　
2018/05/12
　NoMaY氏にアドバイスをいただき、5/1課題に対して以下方針とした。
　・以下ボード依存が無いコード(全く同じになった)なので1階層UPしてマージする。
　　⇒現状維持。
　　　NoMaY氏：フラッシュのブロックサイズが機種毎に異なるため分けておいたほうが後々楽。
　　　　⇒シェルティ：YES。ただ、ブロックサイズはフラッシュモジュールの共通マクロ名で判別できるので
　　　　　将来的にはやはりマージできる可能性もありそう。
　・BSPやドライバは、以下フォルダに入れるのがお作法のようだ。そのうち引っ越しする。
　　⇒現状維持。
　　　NoMaY氏：スマートコンフィグレータの仕様と合わせられない。
　　　　⇒シェルティ：把握。現状維持としたい。
　　　　　他ベンダと似た構成にすべく、継続議論は必要。
　　　　　（スマートコンフィグレータで対応できる方法を考えるなど）
　
　本日の活動は、GitHubへのコード登録。NoMaY氏と相談しひとまずはv1.2.3の現状で登録するのが
　良いであろうとのこと。さしあたり、以下3点を対処すれば現状のものをアップロードできる。
　　(1)AWS接続用アカウント情報(デバイス証明書、秘密鍵)のデータを削除
　　(2)AWS接続用アカウント情報の設定方法、デバイスドライバのインストール方法、
　　　 デモの動作確認方法、改訂履歴などスタートアップガイドを本書の先頭に記す。
　　　 スタートアップガイドは英語、日本語併記とし
　　　 ポーティング記録自体は日本語で良いであろう。
　　(3)ルネサスのデバイスドライバのコードを削除しておく。(NoMaY氏の成果を使わせていただく)
　　
2018/05/01
　種々調整を経て以下4種類のプロジェクトの動作確認が完了。
　Amazon FreeRTOS 1.2.3 と同じ構造に出来た。
　(1)RX65N RSK/CS+
　(2)RX65N RSK/e2 studio
　(3)RX65N Envision Kit/CS+
　(4)RX65N Envision Kit/e2 studio
　
　以下が課題。★
　・AWS IoTのアカウントに紐づいた"モノ"のデバイス証明書、秘密鍵情報を
　　RX65N側に持たせておく必要がある。
　　現在は、以下ソースコードに埋め込んである。
　　　\demos\common\include\aws_clientcredential.h
　　　　・clientcredentialMQTT_BROKER_ENDPOINT[]
　　　　・clientcredentialIOT_THING_NAME
　　　\demos\common\include\aws_clientcredential_keys.h
　　　　・clientcredentialCLIENT_CERTIFICATE_PEM
　　　　・clientcredentialCLIENT_PRIVATE_KEY_PEM
　　　　
　　　ログインするときに必要なデータであるが、実際はこの値はユーザ毎に異なる。
　　　STM32の環境では、システム初回起動時に上記データをコンソールから入力する
　　　方式になっているようだ。正式リリースまでには、真似してシステムを作る必要がある。
　　　（いまのコードはシェルティのアカウントに繋がるのでいたずらしないでくださいね）
　・NIST FIPS140-2では秘密鍵のようにシステムセキュリティの要になるデータを
　　Critical Security Parameter(CSP)と呼称し、適切に定めた暗号境界の中でのみ扱うように
　　定めている。通常のマイコンだと暗号境界が無いためこの要件を満たせないが、
　　RX65N搭載のTrusted Secure IPではこの秘密鍵はもとより、SSL/TLSのセッション鍵に至るまで
　　すべてのCSPをTrusted Secure IPの中(暗号境界の中)で扱えるように設計してある。
　　現状のmbed TLSのコードのままだと、セッション鍵や秘密鍵がデバッガやコード上丸見えであるが、
　　将来これをTrusted Secure IPに秘匿したまま暗号通信が行えるよう改良していく予定。
　・まだデモ「\demos\common」のうち、エコーのデモしか動いてない
　　その他のデモも動作確認していく。特にOTAのデモに着目。
　・e2 studioの環境のフォルダ構成が実物とまだ合ってない。修正する。(CS+はできた)
　・以下はボード依存が無いコード(全く同じになった)なので1階層UPしてマージする。
　　　\lib\ota\portable\renesas\rx65n-envision-kit\aws_ota_pal.c
　　　\lib\ota\portable\renesas\rx65n-rsk\aws_ota_pal.c
　　　\lib\pkcs11\portable\renesas\rx65n-envision-kit\pkcs11.c
　　　\lib\pkcs11\portable\renesas\rx65n-rsk\pkcs11.c
　　　\lib\secure_sockets\portable\renesas\rx65n-envision-kit\aws_secure_sockets.c
　　　\lib\secure_sockets\portable\renesas\rx65n-rsk\aws_secure_sockets.c
　・BSPやドライバは、以下フォルダに入れるのがお作法のようだ。そのうち引っ越しする。
　　　\lib\third_party\mcu_vendor\renesas\
　　　　⇒DriverLibNameとあるので、ベンダが好きな名前を付けられるようだ。
　　　　　何にしようかな？
　　　　　⇒素直に、「rx_driver_package」にしよう。

2018/04/30
　ここ1か月は社内調整に奔走。コードの調整はアメリカの開発部隊に任せた。
　アメリカの開発部隊の調整によりAmazon FreeRTOS Qualification Programの合格に目途が立った。
　また、協力会社との契約は4月は切れており進捗無し。
　5月以降再契約を結びFreeRTOS+TCPへのIGMP機能追加とGCC対応を進めてもらうよう調整した。
　シェルティは、RX65N Amazon FreeRTOS用のボード仕様をW/Wメンバー間で検討。
　ここでは詳細は伏せるがゴールが見えてきた状況。
　デバイスドライバの再配布についてリーガルチームと協議中、
　無線LANモジュール(Silex SX-ULPGN)の日本国内技適取得が大きな課題。
　
　また、セキュリティIP連携やSDIO連携を一旦停止し、
　ボード販売を優先させるよう全体方針を更新。以下進捗表も更新する。

    ------------------------------------
    RX65N Envision Kit、RX65N RSK(2MB版/暗号器あり品)をターゲットにコードメンテを維持します。
    下記 Amazon FreeRTOS 1.2.x は適宜最新コードに更新していきます。
    2018/04/30時点での適用コードは 1.2.3 です。

    ①ルネサスTCP/IPをターゲットで動作させる（Etherの動作確認）
    ②SDIO無線LANを動作確認した時期のFreeRTOS 8.2.2をターゲットで動作させる
    ③ルネサスのFreeRTOSパッケージ、9.0.0をターゲットで動作させる
    ④Amazon FreeRTOS 1.2.xのFreeRTOS部分をターゲットで動作させる
    ⑤Amazon FreeRTOS 1.2.xのFreeRTOS+TCP部分をターゲットで動作させる
    ⑥Amazon FreeRTOS 1.2.xのmbed TLS部分をターゲットで動作させる
    ⑦Amazon FreeRTOS 1.2.xのMQTT部分をターゲットで動作させる（AWSへの接続実験）
    ⑧Amazon FreeRTOS 1.2.xのFreeRTOS+TCP部分のネットワーク層の結合部分を工夫して、
    　(1)Ether、(2)SPI接続無線LANモジュール、(3)SDIO無線LANモジュールの3種類を
    　切り替えられるようにする　★一旦停止、後ほど(2)に絞って再開
    ⑨Amazon FreeRTOS 1.2.xのmbed TLS部分の暗号処理プリミティブの
    　ソフトウェア実装（AESとかRSAとか）をRX65N内蔵暗号器を使った
    　ハードウェア実装に置き換える　★一旦停止
    ⑩Ether層のゼロコピーに対応する　★一旦停止
    ⑪Amazon FreeRTOS本家環境にマージし、Amazon FreeRTOS本家コードへの追従を簡単にできるようにする　★いまここ＠シェルティ
    ⑫Amazon FreeRTOS のGitのforkに登録する
    ⑬Amazon FreeRTOS のCertificationを受験し合格しGitの本家に登録する
    　https://docs.aws.amazon.com/freertos/latest/userguide/freertos-qualification-program.html
    ------------------------------------

　GW期間中は、以下調整を行う。
　(1)RX65N Amazon FreeRTOSコードのマージ(NoMaY氏版、ルネサスアメリカ版、シェルティ版)⇒⑪～⑫
　(2)Amazon Web Serviceの勉強
　(3)Silex SX-ULPGNのドライバ作り⇒⑧の(2)対応 <実際は地ならしだけして5月から弊課に来る研修生に作ってもらう>

　それでは作業開始。まずは(1)から。
　(1)RX65N Amazon FreeRTOSコードのマージ(NoMaY氏版、ルネサスアメリカ版、シェルティ版)⇒⑪～⑫

　作戦を考える。まずは動作確認状況をマトリクス化。
　			NoMaY氏版	アメリカ版	シェルティ版
　ビルド		〇		〇		〇
　正常動作		×		〇		〇
　フォルダ位置非依存	〇		×		〇
　GitHubベース		〇		×		×
　検定合格		×		〇		×
　ベースバージョン	1.2.3		1.2.0?		1.2.3
　
　表を見てみると、NoMaY氏版のプロジェクトにアメリカ版のコードで上書きすれば良さそうだ。
　正常動作したら改めて本家の1.2.3とマージすればよい。
　マージツールでひたすらアメリカ版⇒NoMaY氏版のコードに上書きしていく。
　NoMaY氏のコードは、GitHubから4/29 (Amazon FreeRTOS 1.2.3)にCloneしたもの。
　アメリカ版のコードは、AmazonFreeRTOS_04052018.zipを用いた。
　
2018/03/17
　協力会社に依頼した進捗⑥⑦が戻ってきた。
　3/3分の成果に対し、AWS接続(MQTT実装とSSL/TLS実装)が出来たようだ。
　これで進捗⑥⑦がOKとなった。実機確認し、確かにMQTTでAWSに繋がって
　HELLO WORLDが動いていることを確認。協力会社は現在進捗⑨の調査を進めている。
　
　シェルティはそろそろ⑧をメンテする必要がありそう。
　以下に直近で検討を行った本件の無線LAN対応方針を記す。
　
　SPI接続の無線LANモジュールは主要国で使用/サポート可能なものとしてSilexのSX-ULPGN、
　新興国向けにRealtekのRTL8710を選定。ホビーユース向けにEspressifのESP8266。
　Realtekというとシェルティを組み込みネットワークの世界に誘い込んだ
　あのカニマークのチップ、RTL8019ASを思い出す。
　　https://www.google.co.jp/search?q=rtl8019as&source=lnms&tbm=isch&sa=X&ved=0ahUKEwjDvoyzsvLZAhVDGpQKHVjECycQ_AUICygC&biw=2021&bih=1014
　
　
　SDIO接続の無線LANモジュールは計画通り村田製作所のType 1FX。
　それぞれSDKを入手して実験できるよう手配を進めておく。
　インタフェースはPMODになっていればどのルネサスボードにも
　無改造で接続可能。PMODタイプがあれば尚良し。
　PMODタイプはSPI接続最優先。（UARTだと遅いから）
　SDKがあればSPIでもUSBでもUARTでもなんでもできるジェネリックな感じが良い。
　
　<<SPI接続無線LANモジュール>>
　SilexのSX-ULPGN
　(SDK)：未入手
　　http://www.silexamerica.com/products/connectivity-solutions/embedded-wireless/IoT-Modules/sx-ulpgn-evk/
　(モジュール)：未入手
　　http://www.silexamerica.com/products/connectivity-solutions/embedded-wireless/IoT-Modules/sx-ulpgn-iot-qca4010-radio-module/
　　⇒PMODコンバータを作るか？
　　
　RealtekのRTL8710
　(SDK)：未入手
　　良いのが無い。
　(モジュール)：未入手
　　https://www.seeedstudio.com/RTL8710-WiFi-Module-p-2793.html
　　⇒PMODコンバータを作るか？
　
　EspressifのESP8266
　(SDK)：未入手
　　https://www.mouser.jp/ProductDetail/Olimex-Ltd/MOD-WIFI-ESP8266?qs=QGk6feVlqMKKopUWzCH4tA%3D%3D
　(モジュール)：
　　⇒SDKで十分安いか？

　<<SDIO接続無線LANモジュール>>
　村田製作所のType 1FX
　(SDK)：入手済み（ただし1台のみ。協力会社用にもう1台追加必要）
　　https://www.digikey.jp/product-detail/ja/murata-electronics-north-america/LBWA1KL1FX-TEMP-DS-SD/490-14857-ND/6612483
　(モジュール）：未入手
　　https://wireless.murata.com/eng/products/rf-modules-1/embedded-wi-fi-1/type-1fx.html
　　
　<<無線LANドライバ開発の作戦>>
　SPI接続の無線LANモジュールのドライバ作りは若手の教育素材に良さそう。
　あまり難易度は高くないので、データシート見ながらとにかく作ればOK。

　SDIO接続の無線LANモジュールのドライバ作りは協力会社に依頼する予定。
　Type 1FXはBroadcomのチップセットが搭載されている。Broadcomの無線事業はCypressに
　売却されており、現在無線LANドライバ(WICED)はCypressからオープンソース提供されている。
　Type 1FXの前身であるType ZX用のWICEDは過去FreeRTOS上での動作確認ができたので、
　まずType ZX用のWICEDソフトを用いてType ZXで動作確認を進めてみる。Type ZXのSDKは入手済み。
　Type 1FX対応はWICEDのオープンソースを頑張って自力移植するか
　村田製作所にサポート依頼するか検討。
　
　翻って手元での進捗⑥⑦のマージを行う。
　その後Amazon FreeRTOS本家とのズレ具合を確認する。

　rx65n_rsk_awsで実験開始。

　<<進捗⑥⑦のマージ>>
　まず変化点を分解して構造を把握していき、リポジトリ登録していく。
　まずは定番のgrep調査。
　以降、シェルティ版を本流、協力会社版を支流と表現する。
　
　rx65n_rsk_aws.c
　　メインタスク部分。支流にはAWS接続を行うタスク起動等の処理が追加されている。
　　本流にマージ。
　　以下2関数が追加されている。あとで理解する。★
　　　vApplicationGetIdleTaskMemory()
　　　vApplicationGetTimerTaskMemory()
　　以下関数呼び出しが増えている。あとで理解する。★
　　　SYSTEM_Init()
　　　
　\rx65n_rsk_aws_\src\amazon-freertos-master
　 \demos\common
　　以下ファイル/フォルダが増えている。デモ用コードの様子。本流にマージ。
　　あとで理解する。★
　　　demo_runner
　　　include　　　←インクルードパスを追加しておく
　　　mqtt
　　　tcp
　
　\rx65n_rsk_aws\src\amazon-freertos-master
　 \demos\renesas\rx65n_envision_kit\common\application_code\renesas_code
　  \entropy_hardware_poll.c
　  Amazon FreeRTOSが要求するエントロピーソース(乱数性)の実装。
　  現在は固定値が返るように実装されているが、
　  NetworkInterface.cにget_random_number()関数があるのであとでそこに繋ぐよう変更。
　  最終的にget_random_number()は暗号IPがあるチップのときは暗号IPの乱数器から
　  乱数を取得するように変更する。暗号IPがないチップのときは疑似乱数にする。★
　  
　  ついでに、NetworkInterface.cの uRand()の実装がバグっていたので修正。
　  uint32_t ulRand(void)
    {
	/* 後でハードウェア実装(暗号器使用)に変更します (シェルティ) */
	uint32_t tmp;
	get_random_number(tmp, 4);
	return tmp;
    }
    ↓
　  uint32_t ulRand(void)
    {
	/* 後でハードウェア実装(暗号器使用)に変更します (シェルティ) */
	uint32_t tmp;
	get_random_number(&tmp, 4);
	return tmp;
    }

　\rx65n_rsk_aws\src\amazon-freertos-master
　 \demos\renesas\rx65n_envision_kit\common\config_files
　 　以下コンフィグファイルが増えている。本流にマージ。
　 　aws_bufferpool_config.h
　 　aws_demo_config.h
　 　aws_mqtt_agent_config.h
　 　aws_mqtt_config.h
　 　aws_secure_sockets_config.h
　 　
　 　以下コンフィグファイルが変更されている。本流にマージ。あとで理解する。★
　 　FreeRTOSConfig.h
　 　
　　 　追加：
　　 　#define configSUPPORT_STATIC_ALLOCATION              1

　　　/*********************************************
　　　 * FreeRTOS specific demos
　　　 ********************************************/

　　　/* The address of an echo server that will be used by the two demo echo client
　　　 * tasks.
　　　 * http://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/TCP_Echo_Clients.html
　　　 * http://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/UDP_Echo_Clients.html */
　　　#define configECHO_SERVER_ADDR0       192
　　　#define configECHO_SERVER_ADDR1       168
　　　#define configECHO_SERVER_ADDR2       0
　　　#define configECHO_SERVER_ADDR3       1
　　　#define configTCP_ECHO_CLIENT_PORT    8888

　\rx65n_rsk_aws_\src\amazon-freertos-master
　 \lib
　 　以下フォルダが増えている。本流にマージ。
　 　　bufferpool
　 　　crypto
　 　　mqtt
　 　　pkcs11
　 　　secure_sockets
　 　　third_party
　 　　　\mbedtls\include　←インクルードパスを追加しておく
　 　　　 \mbedtls
　 　　　\pkcs11　←インクルードパスを追加しておく
　 　　tls
　 　　utils
　
　\rx65n_rsk_aws_\src\smc_gen
　　以下フォルダが増えている。これはルネサスのフラッシュAPIのFITモジュールだ。
　　スマートコンフィグレータの機能でフラッシュAPIのモジュールを追加する。
　　r_flash_rx
　 
　ここまでで支流を本流にマージ完了、シェルティの開発サーバにコミットする。(r5128)
　
　<<Amazon FreeRTOS本家とのズレ具合を確認>>
　最新版v1.2.2をダウンロードする。本家と呼称する。
　　https://github.com/aws/amazon-freertos

　amazon-freertos-masterフォルダ全体をgrepして本家と本流の差分確認する。
　\rx65n_rsk_aws\src\amazon-freertos-master\demos
　 \common
　  本流には以下フォルダが足りていない。最終的にはどうするか検討。★
　  　devmode_key_provisioning
　  　greengrass_connectivity
　  　logging
　  　ota
　  　shadow
　
　\rx65n_rsk_aws\src\amazon-freertos-master\demos
　 \renesas\rx65n_envision_kit\common\application_code\renesas_code
　  本家は各マイコン用のBSPや標準デバイスドライバ、main関数、
　  プロジェクトファイル等はここに登録されている。最終的にはルネサスも引っ越す。★
　
　\rx65n_rsk_aws\src\amazon-freertos-master
　　ライセンス関係の以下ファイルが抜けている。登録した。
　　　change_log.txt
　　　directories.txt
　　　LICENSE
　　　README.md
　　　
　\rx65n_rsk_aws\src\amazon-freertos-master\demos
　 \common\include
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　 　(RXマイコン用テストアカウントデータは残す)
　
　\rx65n_rsk_aws\src\amazon-freertos-master
　 \demos\common\demo_runner
　  aws_demo_runner.c
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　 　★マークのところ（協力会社による調整コード）は残す。★
　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS\portable\Renesas\RX600v2
　  port.c
　   インクルードファイルが、iodefine.h(本家)とplatform.h(本流)とで違う。
　   いずれはAmazon本家にかけあい、本家コード修正が必要。★
　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS-Plus-TCP\include
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS-Plus-TCP\source
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS-Plus-TCP\source\portable\BufferManagement
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　 　　BufferAllocation_2.c が大幅に変わっている。要注意。あとで調べる。★
　 　　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS-Plus-TCP\source\portable\Compiler\Renesas
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　 　構造体 pack の調整コード。
　   いずれはAmazon本家にかけあい、本家コード修正が必要。★
　
　\rx65n_rsk_aws\src\amazon-freertos-master\lib
　 \FreeRTOS-Plus-TCP\source\protocols
　 　Amazon FreeRTOS v1.2.2の最新コードに置き換え。
　
　ここまでで本家 v1.2.2を本流にマージ完了。
　シェルティの開発サーバにコミットする。(r5129)
　
　RX65N Envision Kitの環境もメンテする。
　　RX65N Envision KitのほうはDHCPの最初の1回目のパケットが相変わらずコケている。
　　DHCPの再送を待ってDHCP完了してからでないとデモアプリのMQTT通信に
　　失敗するので、rx65n_envision_kit_aws.c においてDEMO_RUNNER_RunDemos()を
　　呼び出すまでのウェイトを2秒から10秒に変更。
　シェルティの開発サーバにコミットする。(r5130)
　

--------------------------------------------------------------------------
2018/03/03
　rx65n_rsk_awsで実験開始。
　開発環境のコンパイラバージョンの表記が間違っていた。修正。V2.07→V2.08。
　
　ルネサスTCP/IP(T4)の関数群を使用している箇所を整備して、
　FreeRTOS+TCPからEtherドライバを直接呼び出すように改良する。

　スマートコンフィグレータの設定から、r_sys_time_rx、r_t4_driver_rx、
　r_t4_rxを削除し、その状態でコード生成を行う。

　ビルドする。ルネサスTCP/IP(T4)に関連する関数呼び出しでエラーになるはず。

　(コンパイルエラー1)
　../src/rx65n_rsk_aws.c(15):E0520005:Could not open source file "r_sys_time_rx_if.h"
　../src/rx65n_rsk_aws.c(17):E0520005:Could not open source file "r_t4_itcpip.h"

　main()付近で呼び出しているT4関連のヘッダ、関数呼び出し、変数等を削除していく。

　<<ここまででコンパイル通った>>

　(リンクエラー1)
　E0562310:Undefined external symbol "_get_random_number" referenced in ".\src\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.obj"
　E0562310:Undefined external symbol "_lan_read" referenced in ".\src\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.obj"
　E0562310:Undefined external symbol "_rcv_buff_release" referenced in ".\src\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.obj"
　E0562310:Undefined external symbol "_lan_open" referenced in ".\src\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.obj"
　E0562310:Undefined external symbol "_lan_write" referenced in ".\src\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.obj"

　ここまでで、NetworkInterface.cの実装のみに絞られた。
　狙い通りT4関連のAPI呼び出しだけになっている。
　→t4_driver.c から関数の中身を持ってくる。
　　UBとかUHとかのITRONのデータ型定義は、uint8_tとかuint16_tとかの標準型に置き換える。
　　
　FreeRTOS_IPInit()で設定されるMACアドレスは、TCP/IP内部RAMに保持される分と
　Etherドライバ経由(R_ETHER_Open_ZC2())でMACのレジスタに保持される分と同じ値に
　する必要がある。FreeRTOS_IPInit()で設定したあとは、どこかの変数に保持されているから
　それをNetworkInterface.cに引き渡す必要があるが、xNetworkInterfaceInitialise()には
　引き渡されてこない。
　STのサンプルを見ると、ucMACAddress[]というグローバル変数で受け渡しをしている。いまいち。
　せめて、FreeRTOSConfig.hにあるコンフィグ値を大元とし、FreeRTOS_IPInit()と
　MAC層に分配してあげるべきであろう。(FreeRTOSIPConfig.hではないのか？これもいまいち）
　
　ここまでの改造で、r_sys_time_rx、r_t4_driver_rx、r_t4_rxを削除し、動作確認もOK。
　rx65n_envision_kit_awsも同じ改造を施し動作確認OK。

　ここまででコミット。(r5091)
　
　NetworkInterface.c に再度着目。課題の整理。過去の課題★のうちNetworkInterface.cのものをサルベージ。
　(1)なぜか lan_write()が-5を返す。あとで確認する。★
　(2)ゼロコピーの概念を無視するが...★
　(3)★後でEther割り込み駆動に必ず直す。
　(4)(送信側のゼロコピーの仕組みが不明。これもまた後で調べる★)
　(5)LANケーブル挿抜のイベントをTCP/IP側に通知する仕組みがあるが...★

　(1)なぜか lan_write()が-5を返す。あとで確認する。★
　　Etherドライバのリンク状態を表す変数「transfer_enable_flag」がONになっておらず
　　最初の1回だけlan_write()が-5を返しているようだ。
　　→xNetworkInterfaceInitialise()が完了時にEtherのリンクアップが完了しているとも限らないので、
　　　何らかFreeRTOS+TCPにリンクアップ/ダウンを通知する仕掛けがあると思うが、見当たらず。
　　　xNetworkInterfaceInitialise()が完了したらリンクアップは完了している前提とする。
　　　
　　　R_ETHER_CheckLink_ZC()でリンクチェックをするのは自分側のPHYの状態であり、
　　　MAC(Etherドライバ)が準備完了しているとは限らない。
　　　なのでEtherドライバからの準備完了のコールバック(callback_link_on())が来てから
　　　xNetworkInterfaceInitialise()を先に進めるようにする。
　　　callback_link_on()がくると、link_detectがETHER_FLAG_ON_LINK_ONになるのでこれで待つ。
　　　
　　　以上から、xNetworkInterfaceInitialise()の流れを整理する。
　　　
　　　整理前：
　　　　(1)lan_open() (MAC/PHYの初期化、オートネゴシエーション開始)
　　　　(2)R_ETHER_CheckLink_ZC()　PHYリンクアップ完了待ち
　　　　(3)ソフトウェアループ　＜適当＞
　　　　(4)受信タスク開始
　　　　(5)MAC層リンクチェック開始
　　　　(6)xNetworkInterfaceInitialise()終了→DHCP送信→xNetworkInterfaceOutput()失敗（まだMAC層準備完了してない）
　　　　　　→DHCPタイムアウト→DHCP再送→xNetworkInterfaceOutput()成功

　　　整理後：
　　　　(1)lan_open() (MAC/PHYの初期化、オートネゴシエーション開始)
　　　　(2)MAC層リンクチェック開始
　　　　(3)MAC層リンク完了待ち
　　　　(4)受信タスク開始
　　　　(5)xNetworkInterfaceInitialise()終了→DHCP送信→xNetworkInterfaceOutput()成功
　　　　　　まだ完ぺきではなくて、動作中にLANケーブルが
　　　　　　抜けたりささったりする動作に対応できてない。(活線挿抜）
　　　　　　現時点で、LANケーブルの挿抜に応じてEtherドライバはコールバックできるが、
　　　　　　これをFreeRTOS+TCPに通知する手段がない。
　　　　　　xSendEventStructToIPTask()で通知できるような気がするので後で調べる。
　　　　　　(5)にあとは任せて、(1)としては完了。
　　　　　　
　(2)ゼロコピーの概念を無視するが...★
　　→後回し。
　(3)★後でEther割り込み駆動に必ず直す。
　　receive_check()タスクでvTaskDelay()で横着しているところをサンプル同様に、ulTaskNotifyTake();を使用する。
　　Ether割り込みはlan_inthdr()に到着するので、ここでvTaskNotifyGiveFromISR()を使って
　　receive_check()タスクにイベント通知する。
　　→ここで実行してみるが、task.cのvTaskNotifyGiveFromISR()の実行時にAssertが発行されてフリーズしてしまう。
　　　割り込みからタスクに通知するのはやはりセンシティブなようだ。OSの機能について調べる必要がある。
　　　→task.cのvTaskNotifyGiveFromISR()の4799行目のAssertに止まっている。
　　　　→ether_receive_check_task_handleが初期化される前に、vTaskNotifyGiveFromISR()を呼んでしまっていた。
　　　　　→ether_receive_check_task_handleに値が入っていたらvTaskNotifyGiveFromISRを呼ぶif文を追加。
　　　　　　→task.cのvTaskNotifyGiveFromISR()の4817行目のportASSERT_IF_INTERRUPT_PRIORITY_INVALID()でフリーズしてしまう。
　　　　　　　→portASSERT_IF_INTERRUPT_PRIORITY_INVALID()を調べてみると以下の通り。
　　　　　　　　現在のIPLがconfigMAX_SYSCALL_INTERRUPT_PRIORITYより小さいとASSERTとなるようだ。
　　　　　　　	#define portASSERT_IF_INTERRUPT_PRIORITY_INVALID() configASSERT( ( get_ipl() <= configMAX_SYSCALL_INTERRUPT_PRIORITY ) )
　　　　　　　	→lan_inthdr()実行中にget_ipl()を呼び出してIPL値を見ると、7となっている。
　　　　　　　	　configMAX_SYSCALL_INTERRUPT_PRIORITYの値は6だった。configMAX_SYSCALL_INTERRUPT_PRIORITYを7に変更。
　　　　　　　	　→ここまでの設定で、動作OKとなった。ping応答もこれまで最大10msのジッターがあったが、
　　　　　　　	　　Ether割り込みとFreeRTOS+TCPを繋いだおかげで、常に1ms以内に応答するようになった。完了。
　(4)(送信側のゼロコピーの仕組みが不明。これもまた後で調べる★)
　　→後回し。
　(5)LANケーブル挿抜のイベントをTCP/IP側に通知する仕組みがあるが...★
　　→課題としては(1)と同じ。

　残った課題は以下。ゼロコピーと活線挿抜である。
　　(2)ゼロコピーの概念を無視するが...★
　　(4)(送信側のゼロコピーの仕組みが不明。これもまた後で調べる★)
　　(5)LANケーブル挿抜のイベントをTCP/IP側に通知する仕組みがあるが...★

　ここまででEnvision KitとRSKのコードを同期させ動作確認し、一旦コミットする。(r5092)

　続いて、ゼロコピーにトライしてみる。
　　BufferAllocation_2.cをビルドから除外し、BufferAllocation_1.c を有効にする。
　　BufferAllocation_1.cを使用するときの vNetworkInterfaceAllocateRAMToBuffers() は何となく実装してあるので
　　ビルドは通る。が、予想通り、エラーメッセージで"INVALID BUFFER"とでる。
　　このときのvNetworkInterfaceAllocateRAMToBuffers()の後を辿っていってみる。

　　2/18に調査した時にたどり着いた、FreeRTOS_IP.cの917行目の分岐が犯人。
　　アライメントが取れてない。
　　
　　ここをクリアするためには、
　　ゼロコピー対応するためのsecond sampleというのを熟読する必要がある。
　　https://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/Embedded_Ethernet_Porting.html#creating_a_zero_copy_network_port_layer

　　何となく分かったが、少し時間がかかりそうだ。次週に持ち込み。
　　
--------------------------------------------------------------------------
2018/02/24
　rx65n_rsk_awsで実験開始。
　ポーティングガイドを見てもう一度方向確認。
　BufferAllocation_2.cで簡易的に実装することにしたので、
　first exampleというのを実装してみる。
　https://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/Embedded_Ethernet_Porting.html#creating_a_simple_network_interface_port_layer

　xNetworkInterfaceInitialise()の構造は特に問題なさそう。
　xNetworkInterfaceOutput()の実装は、送信ディスクリプタの開放が抜けていた。
　　→送信完了後に、vReleaseNetworkBufferAndDescriptor( pxDescriptor );を追加
　
　問題の受信側であるが、NOTE1にBufferAllocation_2.cを使用する場合は
　割り込みの最中にdiscriptorとEthernet buffersの割り当てが行えない、
　と書いてあった。このため、タスクを1個立ち上げてそこで受信割り込みから
　通知を受けた後バッファ割り当てを行い、IPタスクに通知を行うとのこと。
　これはDeferrd Interrupt Handlingといって以下に解説がある。
　https://www.freertos.org/deferred_interrupt_processing.html
　
　これはハードウェアから直接呼び出される割り込み関数では
　割り込み要因の記録とOS層への通知のみを実施し、速やかに割り込み関数を
　終了させるためのメカニズム。
　#OSが存在しない場合は、割り込みコントローラに優先度を設定して
　 多重割り込みを許可する手法で乗り切るが、
　 この仕組みはマイコンの仕組みに依存する。
　 
　割り込み関数からの通知は、deferred interrupt handler taskというので
　処理される。このタスクは通常のアプリケーションタスクより優先度が高い。
　
　When to use deferred interrupt handling：
　このメカニズムは以下3点のようなケースに威力を発揮する。
　・割り込み信号に応じて長い処理が必要
　・割り込み処理内でクリティカルな処理を自力で完全に実装するのが難しいと感じる場合
　　(RTOSが提供するAPIのみで構築したほうが簡単・安全であろう)
　・決まりきった動作をしない処理をさせる場合
　　（何らかの条件により処理時間が伸び縮みする場合）
　　
　→Etherの受信処理はまさに上記ケースに該当する。
　
　Techniques for deferring interrupt processing to a task：
　実装方法は以下2通りとのこと。
　　①1個のタスクで集中管理する（たとえばタイマータスク）
　　「割り込み発生→フラグON→タイマータスク起動→deferred interruptで処理」
　　②アプリがコントロールする（Task Notificationを使用）
　　「割り込み発生→Noticication→deferred interruptで処理」
　　
　　②の利点は割り込み発生から処理実行までのレイテンシが減る、とのこと。
　
　ポーティングガイドのprvEMACDeferredInterruptHandlerTask()のサンプルは
　②を使っているようだ。②を使って実装してみる。
　
　Etherを監視して無限ループするタスクを作る。receive_check()をこのタスクとする。
　
　Ether関連の初期化を行うxNetworkInterfaceInitialise()でタスクを作ればよいであろう。
　xTaskCreate()でタスクハンドルを作り、receive_check()を登録する。
	return_code = xTaskCreate(receive_check, "ETHER_RECEIVE_CHECK_TASK", 100/* stack size (word) */, 0,  configMAX_PRIORITIES, &ether_receive_check_task_handle);
	if(return_code == xTaskCreate)
	{
        	/* The task was created.  Use the task's handle to delete the task. */
        	vTaskDelete( ether_receive_check_task_handle );
	}


　これに伴い、check_ether_link()でreceive_check()を実行していたのをやめる。
　それで、Notifyで受信イベントを受けるのではなくて、
　vTaskDelay()で10msに1回ポーリングする簡易実装にする。
　
　ついでに、xNetworkInterfaceInitialise()でタイマータスクを作ってみる。
　今は、R_CMT_CreatePeriodic()で割り込み関数を定期的に呼び出しているところを
　タイマータスクに置き換える。
　https://www.freertos.org/FreeRTOS-timers-xTimerCreate.html
　
　xTimerCreate()でタイマーハンドルを作って、それをxTimerStart()に入力する感じか。
　
　timer_handle = xTimerCreate("ETHER_TIMER", 10, pdTRUE, &timer_id, check_ether_link);
　xTimerStart(timer_handle, 0);
　
　といったところか。未定義の変数はグローバルで定義しておく。
　これで、receive_check()がFreeRTOS配下のタスクとして呼び出された。
　
　ポーティングガイドのprvEMACDeferredInterruptHandlerTask()のサンプルに従って
　API呼び出し順序を確かめていく。
　
　・  ulTaskNotifyTake()
　　→これは上記「②アプリがコントロールする」場合に必要なイベント通知受付口。
　　　今回はvTaskDelay()を使って横着しているので不要。
　・ pxGetNetworkBufferWithDescriptor( xBytesReceived, 0 );
　　→受信データ長に応じたバッファを確保して、ディスクリプタを生成して戻り値で
　　　返してくれるAPI。
　　　RXマイコンのEtherコントローラドライバは、lan_read()の戻り値で受信データ長を
　　　戻してくれる。received_data_sizeに入れておく。
　　　また、引数のポインタに、バッファポインタを書いてくれる。
　　　memcpy()でコピーすればFreeRTOS+TCP側のバッファにコピーすればよいであろう。
　　　（あとでゼロコピー対応に進化させる）
　・ディスクリプタへのデータ設定、イベント通知用の構造体の設定、特に問題なさそう
　				pxBufferDescriptor->xDataLength = received_data_size;
				xRxEvent.eEventType = eNetworkRxEvent;
				xRxEvent.pvData = pxBufferDescriptor;

　実行して確認してみるも、やはりpxGetNetworkBufferWithDescriptor()が正常終了しない。
　pxGetNetworkBufferWithDescriptor()に潜って再確認していく。
　
　なんかセマフォが解放されてない様子？
　送信側xNetworkInterfaceOutput()でディスクリプタを確保して送信完了したときに
　リリースバッファのAPIを呼んでいるはずだが・・・？
　
　なぜかlan_write()が送信成功しているのに-5を返していて、if文が偽になっていた。
　暫定で偽のときもリリースバッファを呼ぶようにした。
　
　	return_code = lan_write(0, tmp_buf, 14, tmp_buf + 14, pxNetworkBuffer->xDataLength - 14);
	if(return_code > 0)
	{
		/* Call the standard trace macro to log the send event. */
		iptraceNETWORK_INTERFACE_TRANSMIT();

		vReleaseNetworkBufferAndDescriptor(pxNetworkBuffer);
	}
	else
	{
		/* なぜか lan_write()が-5を返す。あとで確認する。★ */
		vReleaseNetworkBufferAndDescriptor(pxNetworkBuffer);
	}
	
　ここまでの実装でDHCPシーケンスが完了するようになった。
　ping応答もできている。無事FreeRTOS+TCPの移植完了！！！！
　（★課題山盛りですが）
　
　RSKで動作確認していたので、Envision Kit側にもネットワークインタフェースのコードを
　登録してコミット。(r5066)
　
--------------------------------------------------------------------------
2018/02/18
　rx65n_envision_kitで作業開始。
　
　どうにもデバッガが重たい。FreeRTOS用のスタック(FreeRTOSConfig.hで設定)が
　足りていないような気がする。FreeRTOSがシステムスタック側に影響しているか？

　現在のRX65NのRAM使用状況を変更してみる。
　後でGUIを載せたときにチラつき防止のためダブルバッファにしたかったが致し方なし。

　0x00000000番地(256KB)：液晶バッファ1
　0x00800000番地(256KB)：液晶バッファ2
　0x00840000番地(128KB)：システム領域
　↓
　0x00000000番地(256KB)：システム領域(Bセクション(FreeRTOSスタック、ヒープ、その他変数等))
　0x00800000番地(256KB)：液晶バッファ2
　0x00840000番地(128KB)：システム領域(Bセクション以外(システムスタックやEtherバッファ等))

　これで、デバッガ重たい現象が改善された。
　main()ループにvTaskDelay(10000);を入れて無限ループさせ、
　main()ループが生きてるか確認するメッセージを出力するようにした。
　
　安定稼働しているようだ。ただしまだDHCP Discoverパケットを
　出力するための送信関数xNetworkInterfaceOutput()は呼ばれないようだ。

　ただし定常的にFreeRTOSかFreeRTOS+TCPからは謎のログ(文字化けしている？)は出力されている。(★調べる)→OK
　何やらステートマシンは動き続けている様子だ。

　ひとまず安定したので、いったんコミットする。(r5008)

　メッセージの文字化けの原因はきっと、#include <stdio.h> が無いからだ。
　FreeRTOS本体のコードでインクルードするわけにもいかないが、幸いコンフィグファイルは
　ユーザ定義部分に吐き出されている格好なのでそちらに#include <stdio.h>を追加。
　\rx65n_envision_kit_aws\src\amazon-freertos-master\demos\renesas\rx65n_envision_kit\common\config_files
　　FreeRTOSConfig.h
　　FreeRTOSIPConfig.h

　→無事、FreeRTOSとFreeRTOS+TCPのシステムログが見れるようになった。
　　エラー時のトレースログもだせるみたいなので、あとでこれも出力に繋いでみよう。
　　液晶表示が賑やかになってきた。
　　バックログが見えるように、UARTでも出力したほうがよい。
　　RSKは標準でUARTがUSBシリアル変換されてUSBから出てくるが、
　　Envision Kitはその仕掛けがない。（E2OBの機能はデバッガ使用時はUART出力できないので却下）
　　Envision KitはPMODにSCI2が配線されていて、PMODモジュールでUSBシリアル変換があるから
　　それを付ければUARTをUSBから出せる。（前に試してちゃんとできた）
　　　→https://store.digilentinc.com/pmod-usbuart-usb-to-uart-interface/
　　　　→これをEnvision KitのCH14の1-6に挿せばよい。
　　　　　SCI2をUARTモードで使用すればPCにシステムログを送れる。
　　　　　コードでいうと、lcd_conf.hで my_sw_charput_function()がprintf()経由BSPから呼ばれるが、
　　　　　今はここに液晶に1文字出力するようにしているところがあり、ここに並行してSCIから出力する
　　　　　ようにコード追加すればよい。(★後でメンテ)

　さて液晶表示のシステムログだけでもある程度何が起きているか分かるようになった。
　システムログ内容を紐解いてみる。
　　→案の定、DHCP discoverプロセスが、応答がなくてタイムアウトして、リトライ制御をし続けている。
　
　ディスクリプタを4個設定にしたのに、(now59)とか表示されてるので、ディスクリプタ周りの調整が
　何らか足りてないようだ。そもそも送信関数(xNetworkInterfaceOutput())すら呼ばれてないので、
　送信処理の最初の方でこけてそう。
　確か昨日、FreeRTOSIPConfig.hで60をEtherドライバ側の定義ETHER_CFG_EMAC_TX_DESCRIPTORS（中身は4)を
　読み込むようにしたはずだが・・・？
　
　FreeRTOSIPConfig.hを確認したらいつの間にかデフォルトの60に戻ってた。
　ガチャガチャやっててデフォルトで上書きしてしまったようだ。もう一度修正。
　
　期待通り(now59)の表示は(now3)となった。依然としてxNetworkInterfaceOutput()は呼ばれない。
　何かを見落としているか。
　
　FreeRTOS+TCPのIP層の実装(FreeRTOS_TCP_IP.c)を確認していく。
　xNetworkInterfaceOutput()を呼び出しているのは950行目1か所のみ。
　コメントに /* Send! */ と書いて有って気合が入っているので間違いないだろう。
　
　この呼び出し口の実装は、prvTCPReturnPacket()。この関数の先頭にブレークを
　しかけるも、反応なし。上位に上っていく。
　
　FreeRTOS_TCP_IP.c の実装に関数呼び出し順が記載されている。ありがたい。
　prvTCPReturnPacket()を呼び出しているところを片っ端からブレーク貼って網をはる。
　prvTCPSendRepeated()、prvTCPPrepareSend()、prvTCPHandleState()の先頭にブレークはる。
　
 * IP-Task:
 *		xTCPTimerCheck()				// Check all sockets ( declared in FreeRTOS_Sockets.c )
 *		xTCPSocketCheck()				// Either send a delayed ACK or call prvTCPSendPacket()
 *		prvTCPSendPacket()				// Either send a SYN or call prvTCPSendRepeated ( regular messages )
 *		prvTCPSendRepeated()			// Send at most 8 messages on a row
 *			prvTCPReturnPacket()		// Prepare for returning
 *			xNetworkInterfaceOutput()	// Sends data to the NIC ( declared in portable/NetworkInterface/xxx )
 
  *	xProcessReceivedTCPPacket()
 *		prvTCPHandleState()
 *			prvTCPPrepareSend()
 *				prvTCPReturnPacket()
 *				xNetworkInterfaceOutput()	// Sends data to the NIC
 *		prvTCPSendRepeated()
 *			prvTCPReturnPacket()		// Prepare for returning
 *			xNetworkInterfaceOutput()	// Sends data to the NIC
 
 
　結果、どこにもブレークしない。
　
　そもそもIPタスクに送信要求が届いてないのではないか。
　DHCPプロセスからIPタスクに送信要求を出す方向から見直してみる。
　
　DHCPプロセスからIPタスクに対する送信要求は、FreeRTOS_DHCP.cの
　926行目のFreeRTOS_sendto()と思われる。この中を確認していく。
　
　進んでいくと、FreeRTOS_Socket.cの855行目の
　pxUDPPayloadBuffer_to_NetworkBuffer()が呼ばれる。
　ここまでの処理にエラーなどは発生していない様子。
　
　FreeRTOS_IP.cの917行目の分岐にたどり着いた。
　if( ( ( ( uint32_t ) pucBuffer ) & ( sizeof( pucBuffer ) - 1 ) ) == 0 )が
　偽になるため、バッファポインタが登録されずpxResultにNULLがセットされ
　抜けてしまう。これが原因か。
　
　2/17に適当に実装したvNetworkInterfaceAllocateRAMToBuffers()が原因か。

　上記if()文の条件を確認すると、何やら送信バッファのアライメントが
　取れているかどうかを確認するためのものの様子。
　
　少し巻き戻って、FreeRTOS_Socket.cの829行目の条件分岐で以下ある。
　if( ( xFlags & FREERTOS_ZERO_COPY ) == 0 )
　
　これでFREERTOS_ZERO_COPYがONのほうに流れていっているのが原因のようだ。
　ゼロコピー実装は後回しにすると決めたので、なんでゼロコピーが有効に
　なっているのか調べる。
　
　FreeRTOS_DHCP.cの926行目をよくみると、FREERTOS_ZERO_COPYを直接指定していた。
　ということは、DHCPを使用するときはゼロコピー必須ということ。
　if( FreeRTOS_sendto( xDHCPData.xDHCPSocket, pucUDPPayloadBuffer, ( sizeof( DHCPMessage_t ) + xOptionsLength ), FREERTOS_ZERO_COPY, &xAddress, sizeof( xAddress ) ) == 0 )

　DHCP機能はさすがに切ることはできないので、
　先にゼロコピーの実装を済ませたほうが良さそうだ。
　
　Amazon FreeRTOS全文でZERO_COPYでGrep。PICのサンプルに以下2行を発見。
　これをRX側のFreeRTOSIPConfig.hに入れる。
　#define ipconfigZERO_COPY_TX_DRIVER              ( 1 )
　#define ipconfigZERO_COPY_RX_DRIVER              ( 1 )
　
　あと、#include "pack_struct_start.h"と#include "pack_struct_end.h"に挟まれた構造体の
　typedefに他コードからのシンボル参照(Ctrl+左クリック)ができず、エラー表示になっている。
　コンパイルは通るのでコンパイル前処理の構文解析でエラーになっている感じ。
　→★ツール開発部門に問い合わせてみる。
　
　翻って手元の実装。
　FreeRTOS_IP.cの917行目の分岐をもう一度見てみる。これが通らないと先に進まない。
　　if( ( ( ( uint32_t ) pucBuffer ) & ( sizeof( pucBuffer ) - 1 ) ) == 0 )

　ここに最初に到達した時のpucBufferの値は、0x84f716。
　この値がポインタサイズ(4)から1を引いた値でマスクを取り
　何かが残ったら（＝4バイトアライメント取れてなければ）偽。
　0x84f716が4の倍数になっていなければ通らないということ。
　このケースだと4の倍数になってないので通らない。
　
　この値がどこから来ているかというと、
　FreeRTOS_DHCP.cの926行目のpucUDPPayloadBufferである。
　このポインタは、921行目のprvCreatePartDHCPMessage()で出力される。この中身を探る。
　バッファ領域は、FreeRTOS_GetUDPPayloadBuffer()で取得するようだ。この中身を探る。

　このバッファ領域は、BufferAllocation_1.cから割り当てられている様子なので、
　BufferAllocation_1.c をビルドから除外、BufferAllocation_2.cをビルド対象とする。
　BufferAllocation_2.c はゼロコピー用のメモリ割り当て機構だ。
　
　ここまでの実装で、xNetworkInterfaceOutput()に送信データが引き渡されるようになった。

　なお、送受信バッファの取り扱いは要注意だ。
　FreeRTOSIPConfig.h に、 ipconfigPACKET_FILLER_SIZEというマクロが2で設定されている。
　これは、Etherパケットが以下構成になっていて、IPヘッダ以降が32ビットアライメント取れていない
　問題に起因する。これは世界共通の問題であり、通常MAC層でEtherヘッダとIPヘッダの間に2バイト
　パディングを挟み込んで解決している。（あるいはデータをコピーしなおしたり何らかのペナルティを背負って実装）
　RXマイコンのEtherMACは幸いこのパディング機能を持っているのでソフト次第で上手に解決できるはず。
　
　Etherパケット構成
　[ETHER_HEADER(14 byte)][IP_HEADER(20 byte)][TCP_HEADER(20 byte)][PAYLOAD(0-1460 byte)]
　↓実際にハードウェアが受信データをメモリ展開する際
　[ETHER_HEADER(14 byte)][IP_HEADER(20 byte)][TCP_HEADER(20 byte)][PAYLOAD(0-1460 byte)]・・・工夫無し
　[ETHER_HEADER(14 byte)][pad(2 byte)][IP_HEADER(20 byte)][TCP_HEADER(20 byte)][PAYLOAD(0-1460 byte)]・・・工夫有り
　
　ひとまず現状の構成でどのようにこの辺りが解釈されているか確認しつつ、送信側の実装を進めていく。
　
　単純にxNetworkInterfaceOutput()に渡ってきたデータを
　t4_driver.cが持っている lan_write() 関数に引き渡してみる。
　
　ゼロコピーの概念を無視するが、たぶん、xNetworkInterfaceOutput()で渡されるデータは
　Ether送信バッファのポインタであるため、いったんテンポラリに格納してから
　Etherドライバに渡すことにする。歪だがまだ全貌が分からないので仕方ない。あとで必ず直す。★
　
　ここまでで、RX65Nから、DHCP discoverパケットが出力できるようになった。Wiresharkで確認済。
　DHCPサーバからDHCP offerパケットが返ってきたので、正しいDHCP discoverとして扱われたようだ。
　RX65N側はこれをまだ受ける口を付けてないので、これ以上はDHCPシーケンスは進んでいない。
　
　MAC層で受信からのEDMAC転送は完了して割り込みは発生しているので、
　この割り込みをキャッチしてFreeRTOS+TCP側に受信割り込みイベントを伝える口を
　つけてやればいいはずだ。
　
　ポーティングガイドを見てみる。
　xSendEventStructToIPTask()で受信割り込みイベントを通知すればいいようだ。

　割り込みイベントはt4_driver.c の lan_inthdr()まで上がってきているはずだが
　t4_driver.c は最終的には不要。r_ether_rxのAPIを直接NetworkInterface.cから
　呼び出してあげればよい。今はとりあえずでEther割り込みではなく、
　リンク状態を定期的に調べる check_ether_link() で受信データがあった場合に
　FreeRTOS+TCPのxSendEventStructToIPTask()を呼び出すコードを追加する。
　★後でEther割り込み駆動に必ず直す。
　
　汚い実装だが、ひとまず受信ディスクリプタは正常に回転し始めた。
　受信リクエストを受け取ったFreeRTOS+TCPは、「CANNOT ADD 1」とメッセージを吐いている。
　
　受信したらpxGetNetworkBufferWithDescriptor()でバッファ/ディスクリプタを確保して
　ディスクリプタにバッファポインタと受信データ長を書き込んでxSendEventStructToIPTask()で
　渡せば良いようだ。
　
　今一度、ポーティングガイドのバッファ管理の項をよく読んでみる。
　https://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/Embedded_Ethernet_Buffer_Management.html
　
　BufferAllocation_1.c はEtherバッファが静的にEtherドライバ内部にある場合、
　BufferAllocation_2.c はEtherバッファが動的にヒープから確保される場合、とある。

　ゼロコピーを使うか使わないかと勘違いしていたが、そうではなかった。
　BufferAllocation_1.c を使うようにする。
　
　vNetworkInterfaceAllocateRAMToBuffers()の実装体は送信バッファポインタを
　渡すようにしていたが、受信バッファのポインタを渡すように変更した。
　(送信側のゼロコピーの仕組みが不明。これもまた後で調べる★)
　
　BufferAllocation_1.cに変更したことで、ディスクリプタの初期値に不足がある様子。
　何やら受信リクエストをxSendEventStructToIPTask()で飛ばす前に
　pxGetNetworkBufferWithDescriptor()を実行するとおかしくなる。
　vNetworkInterfaceAllocateRAMToBuffers()の実装を見直す必要がありそう。
　
　動作としては安定しているのでひとまずコミットする。(r5009)
　→ただしDHCP送信はできなくなっている。おそらくディスクリプタの不調。
　　xNetworkInterfaceOutput()も呼ばれていない状態。
　
　rx65n_rsk 側にコードを反映した。(r5010)
　
　ひとまず、BufferAllocation_2.cを使うことにして、
　全体動作を確認することを優先することにする。
　DHCP送信まで出来ることを確認。
　受信についてもイベント通知はOS層まで届いているが
　ディスクリプタ内の受信バッファポインタが異常値なので
　データの受け渡し方法に問題があるようだ。(r5011)

--------------------------------------------------------------------------
2018/02/17
　rx65n_envision_kitで作業開始。

　NoMaY氏からの情報でAmazon FreeRTOSが 1.2.0 にバージョンアップされているとのこと。
　1.2.0のコードをダウンロードし、差分確認。
　NoMaY氏の情報通り、MQTT周りのセキュリティ実装が追加されている様子。
　RX65Nに移植済みのFreeRTOS本体部分は特に影響なし。
　リポジトリ内のコードを1.2.0のものに置き換えていく。

　そういえばバージョン表記がきになる。"version"でAmazon FreeRTOS全体をgrepしてみた。
　Amazon FreeRTOS全体を包含するバージョン定義はまだないようだ。
　Amazon FreeRTOS 1.2.0 に内包するソフトの主要なバージョンは以下の通り。
　・アプリ：v0.9.0
　　\amazon-freertos-master\demos\common\include\aws_application_version.h(29,13)  [SJIS]: #define APP_VERSION_MAJOR  0
　　\amazon-freertos-master\demos\common\include\aws_application_version.h(30,13)  [SJIS]: #define APP_VERSION_MINOR  9
　　\amazon-freertos-master\demos\common\include\aws_application_version.h(31,13)  [SJIS]: #define APP_VERSION_BUILD  0
　・mbed TLS：v2.6.0
　　\amazon-freertos-master\lib\third_party\mbedtls\include\mbedtls\version.h(40,17)  [SJIS]: #define MBEDTLS_VERSION_MAJOR  2
　　\amazon-freertos-master\lib\third_party\mbedtls\include\mbedtls\version.h(41,17)  [SJIS]: #define MBEDTLS_VERSION_MINOR  6
　　\amazon-freertos-master\lib\third_party\mbedtls\include\mbedtls\version.h(42,17)  [SJIS]: #define MBEDTLS_VERSION_PATCH  0
　・PKCS11：v2.40.0
　　\amazon-freertos-master\lib\third_party\pkcs11\pkcs11t.h(14,18)  [SJIS]: #define CRYPTOKI_VERSION_MAJOR 2
　　\amazon-freertos-master\lib\third_party\pkcs11\pkcs11t.h(15,18)  [SJIS]: #define CRYPTOKI_VERSION_MINOR 40
　　\amazon-freertos-master\lib\third_party\pkcs11\pkcs11t.h(16,18)  [SJIS]: #define CRYPTOKI_VERSION_AMENDMENT 0
　・FreeRTOSカーネル：v10.0.1
　　\amazon-freertos-master\lib\include\task.h(46,19)  [SJIS]: #define tskKERNEL_VERSION_NUMBER "V10.0.1"
　　\amazon-freertos-master\lib\include\task.h(47,19)  [SJIS]: #define tskKERNEL_VERSION_MAJOR 10
　　\amazon-freertos-master\lib\include\task.h(48,19)  [SJIS]: #define tskKERNEL_VERSION_MINOR 0
　　\amazon-freertos-master\lib\include\task.h(49,19)  [SJIS]: #define tskKERNEL_VERSION_BUILD 1
　・FreeRTOS+TCP：無し？

　作業に戻る。

　とにかく「FreeRTOS-Plus-TCP」をプロジェクト登録してみる。
　「\FreeRTOS-Plus-TCP\source\portable」にデバイス毎の独自部分を
　独自作成する必要がある。バッファ管理「BufferManagement」コンパイラ毎定義「Compiler」
　ネットワーク層「NetworkInterface」の3種類を独自作成しなければならない。

　http://japan.renesasrulz.com/cafe_rene/f/forum21/4772/amazon-freertos-rx/26876#26876
　上記URLのNoMaY氏の先行調査を頭に入れながら、コンパイル開始。

　(コンパイルエラー1)FreeRTOS+TCP関連のヘッダファイル見つからない
　　→「\amazon-freertos-master\lib\FreeRTOS-Plus-TCP\include」にインクルードパスを通す
　(コンパイルエラー2)"FreeRTOSIPConfig.h"が見つからない
　　→「\amazon-freertos-master\demos\vendor\board\common\」にあるようだ。
　　　ベンダ毎のBSPのコンフィグに入れると良いようだ。
　　　「\rx65n_envision_kit_aws\src\smc_gen\r_config」に入れておく。]
　　　　★あとで \amazon-freertos-master\demos\renesas\rx65n_envision_kit\common\config_files 
　　　　　にFreeRTOSのコンフィグを引越し。→完了
　(コンパイルエラー3)"pack_struct_start.h"が見つからない
　　→これは、TCP/IPのヘッダを表す構造体に pack オプションを付けるための
　　　マルチコード対応用のヘッダ。
　　　「\rx65n_envision_kit_aws\src\FreeRTOS-Plus-TCP\source\portable\Compiler\Renesas」にインクルードパスを通す
　(SH用コードが実装されているので、RX用コードに変更/NoMaY氏の先行調査参照)
　　→"pack_struct_start.h", "pack_struct_end.h"
　(コンパイルエラー4)"FreeRTOS_HTTP_commands.h"が見つからない
　　→「\rx65n_envision_kit_aws\src\FreeRTOS-Plus-TCP\source\protocols\include」ににインクルードパスを通す
　(コンパイルエラー5)"ff_stdio.h"が見つからない
　　→"\rx65n_envision_kit_aws\src\FreeRTOS-Plus-TCP\source\protocols\HTTP\FreeRTOS_HTTP_server.c"
　　　エラー元はこのファイル。
　　　FTPサーバのコードからファイルシステム系のソフトが呼び出されている様子。
　　　今はまだFTPサーバ機能は要らないのでコード自体をプロジェクトから除外しておく。
　　　TCP/IPの上位にあたるプロトコル群（HTTPとFTPとNTPとサーバ設置用コード）に関する以下ファイルをプロジェクトから除外。
　　　・FreeRTOS_HTTP_server.c
　　　・FreeRTOS_HTTP_commands.c
　　　・FreeRTOS_FTP_server.c
　　　・FreeRTOS_FTP_commands.c
　　　・FreeRTOS_TCP_server.c
　　　・NTPDemo.c
　　(コンパイルワーニング1)
　　　→packオプション周りのワーニングがいっぱいでるので、NoMaY氏の先行調査を参考に修正。
　　
　　<<ここまででコンパイル通った>>
　　
　　(リンクエラー1)
　　　E0562300:Duplicate symbol "_uxGetMinimumFreeNetworkBuffers"
　　　　→バッファ管理「BufferManagement」に2個同じようなファイルが入っているのが原因であろう。
　　　　　中身はあとで確認するとして、BufferAllocation_2.cをビルドから除外しとく。
　　　　　
　　(リンクエラー2)
　　　E0562310:Undefined external symbol "_ulRand" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DHCP.obj"
　　　E0562310:Undefined external symbol "_ulRand" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_Sockets.obj"
　　　E0562310:Undefined external symbol "_pcApplicationHostnameHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DHCP.obj"
　　　E0562310:Undefined external symbol "_vNetworkInterfaceAllocateRAMToBuffers" referenced in ".\src\FreeRTOS-Plus-TCP\source\portable\BufferManagement\BufferAllocation_1.obj"
　　　E0562310:Undefined external symbol "_xApplicationDNSQueryHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DNS.obj"
　　　E0562310:Undefined external symbol "_vApplicationIPNetworkEventHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_IP.obj"
　　　E0562310:Undefined external symbol "_xNetworkInterfaceOutput" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_ARP.obj"
　　　E0562310:Undefined external symbol "_xNetworkInterfaceOutput" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_IP.obj"
　　　E0562310:Undefined external symbol "_xNetworkInterfaceOutput" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_TCP_IP.obj"
　　　E0562310:Undefined external symbol "_xNetworkInterfaceOutput" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_UDP_IP.obj"
　　　E0562310:Undefined external symbol "_xNetworkInterfaceInitialise" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_IP.obj"

　　　→ネットワーク層(IP層)とデータリンク層(Ether層)のインタフェースの実装体が無い感じ。
　　　　これはFreeRTOS+TCPのポーティングガイドに従って実装すればよさげ。
　　　　ラッキーなことに、SH2A用のNetworkInterface.cが用意されているではないか。（AmazonがSH2Aでトライアルしたのかな？）
　　　　SH2AとRXのEtherコントローラは同じで、Etherドライバも似た感じなので、SH2A用のコードを拝借して、
　　　　以下ファイルを作成。
　　　　\rx65n_envision_kit_aws\src\FreeRTOS-Plus-TCP\source\portable\NetworkInterface\RX\NetworkInterface.c
　　
　　<<新たなコードを追加したのでコンパイルエラー発生>>

　　(コンパイルエラー6)
　　　E0520005:Could not open source file "hwEthernet.h"
　　　　→RXマイコンのEtherドライバのヘッダファイルは、r_ether_rx_if.hである。変更。
　　
　　(コンパイルエラー7)
　　　E0520020:Identifier "NetworkBufferDescriptor_t" is undefined
　　　　→Amazon FreeRTOS全体をgrepすると、FreeRTOS_IP.h に定義があった。
　　　　　→NetworkInterface.cに #include "FreeRTOS_IP.h" を足してあげる。
　　　　
　　(コンパイルエラー8)
　　　E0520136:Struct "xNETWORK_BUFFER" has no field "pucBuffer"
　　　　→xNETWORK_BUFFERにはpucBufferは無いようだ。
　　　　　このエラーはvEMACCopyWrite()関数内のものであるので、きっと送信ができなくなる
　　　　　だろうけれど、ひとまずコメントアウトしておく。
　　　　
　　<<ここまででコンパイル通った>>

　　(リンクエラー3)
　　　(リンクエラー2)と比較して、_xNetworkInterfaceOutput()、_xNetworkInterfaceInitialise()のリンクエラーが消えた。
　　　だけれど、まだ大半のインタフェース関数が未実装。SH2A版のコードはトライアル早々に諦められたようだ。
　　　今は空関数を作っておいて、あとで動かしつつポーティングガイドを見ながら実装してみる。
　　　関数の定義はポーティングガイドにあるはずだ。NoMaY氏のメモを見る。以下参考になりそう。
　　
　　　Porting FreeRTOS+TCP to a Different Microcontroller
　　　http://www.freertos.org/FreeRTOS-Plus/FreeRTOS_Plus_TCP/Embedded_Ethernet_Porting.html
　　　
　　　ざっと見ると、性能を出すためには、このポーティングガイドを本気で読む必要がある。
　　　単に動かすだけならとにかく関数同士をつないであげれば良さそう。
　　　必要なAPIはすでにRX用のEtherドライバに有る感じ。
　　　無線LAN対応時もここの実装がキモになる。
　　　
　　　_xNetworkInterfaceOutput()と、_xNetworkInterfaceInitialise()が真にFreeRTOS+TCPから
　　　呼ばれるインタフェースのようだ。他のはどうだろうか。
　　　コードのくっつき具合から判定していく。
　　　
　　E0562310:Undefined external symbol "_ulRand" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DHCP.obj"
　　E0562310:Undefined external symbol "_ulRand" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_Sockets.obj"
　　　→関数名から、乱数を取得するための関数を期待しているようだ。
　　　　NetworkInterface.cに空関数を用意しておく。あとで中身をつくる。
　　　　ルネサスTCP/IPのt4_driver.cに疑似乱数を生成する似たような関数が有るのでそれを持ってくる。
　　　　最終的にはRX65N内蔵の暗号器にある乱数発生器のAPIを使うとよいであろう。
　　　　
　　　　関数プロトタイプは uint32_t ulRand(void); FreeRTOSIPConfig.h にexternで宣言がある。
　　　　NetworkInterface.cに実体、NetworkInterface.hにプロトタイプ宣言を置けばよいかな。
　　　　
　　E0562310:Undefined external symbol "_pcApplicationHostnameHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DHCP.obj"
　　　→ポーティングガイドに載ってないので、Amazon FreeRTOS全文grepから予想。
　　　　DHCPでホスト名を登録する機能があるが、ホスト名をユーザ定義関数で引き渡せる仕組みのようだ。
　　　　DHCP動作中にこの関数が呼ばれてユーザが指定した名前がDHCPにより取得される。
　　　　FreeRTOS+TCPコンフィグ(FreeRTOSIPConfig.h)でON/OFFできる。
　　　　#define ipconfigDHCP_REGISTER_HOSTNAME           1
　　　
　　　　いくつかのサンプル(PIC用、Win用）でmain.cに実装体があった。
　　　　コメントを読むと、DHCPでユーザの名前をネットワークに登録する際に
　　　　DHCPのコードがそのユーザの名前を読み込むときに呼び出すユーザ定義関数である。
　　　　まあmain関数付近に実装しておくのが妥当。
　　　　
　　　　以下PICのサンプル。LLMNR、NBNSがOFF、DHCP_REGISTER_HOSTNAMEがONのときに必要な関数。
　　　　以下PICのコードをそのままmain付近(rx65n_envision_kit_aws.c)に持ってくる。
　　　　IPコンフィグでLLMNR、NBNSはOFFにしておく。
　　　　#include "FreeRTOSIPConfig.h"のインクルードも追加しておく。
　　　　
　　　　#if ( ipconfigUSE_LLMNR != 0 ) || ( ipconfigUSE_NBNS != 0 ) || ( ipconfigDHCP_REGISTER_HOSTNAME == 1 )
　　　　const char * pcApplicationHostnameHook( void )
　　　　{
　　　　    /* Assign the name "FreeRTOS" to this network node.  This function will
　　　　     * be called during the DHCP: the machine will be registered with an IP
　　　　     * address plus this name. */
　　　　    return "RX65N_FREERTOS_TCP_TEST_BY_SHELTY";
　　　　}
　　　　#endif

　　E0562310:Undefined external symbol "_vNetworkInterfaceAllocateRAMToBuffers" referenced in ".\src\FreeRTOS-Plus-TCP\source\portable\BufferManagement\BufferAllocation_1.obj"
　　　→ポーティングガイドに載ってる。
　　　　BufferAllocation_1.cのみを使用する場合に必要になる関数のようだ。
　　　　先ほど、BufferAllocation_2.cはビルド対象外にしたが、このバッファ確保をうまく使いこなせば、
　　　　性能向上が出来る感じ。たぶん、Ether層からデータを吸い上げる時にTCP/IP層に対して
　　　　データコピーで渡すか、ポインタで渡すか（ゼロコピー）切り替えるものだ。
　　　　ただしゼロコピーは実装が面倒。RXマイコンのEtherドライバはゼロコピー対応なので、
　　　　あとでじっくり性能評価しながら作り込みをしてみる。
　　　　性能はあとで改善するとして、今はvNetworkInterfaceAllocateRAMToBuffers()を実装しておく。
　　　　実装体は後で考えるとして、今はvNetworkInterfaceAllocateRAMToBuffersを空にしておく。
　　　
　　E0562310:Undefined external symbol "_xApplicationDNSQueryHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_DNS.obj"
　　　→いつの間にか消えてた。たぶん"pcApplicationHostnameHook"の対処あたりと関係しているようだ。
　　　　後で調べる。
　　　　
　　E0562310:Undefined external symbol "_vApplicationIPNetworkEventHook" referenced in ".\src\FreeRTOS-Plus-TCP\source\FreeRTOS_IP.obj"
　　　→最後の1個だ。
　　　　ポーティングガイドに載ってないので、Amazon FreeRTOS全文grepから予想。
　　　　PICのサンプルがヒット。IP層からのイベント通知用の様子。
　　　　コードを見ると、DHCP処理が完了した時のコールバックが書かれてる感じ。
　　　　他にもいろいろなイベントが飛んできそう。PICのコードをmain付近(rx65n_envision_kit_aws.c)に持ってくる。
　　　　ネットワークインタフェースを作り込んだときの動作確認に役に立つであろう。
　　　　
　　　　PIC特有の以下コードは除外しておく。
　　　  /* The network is up so we can run. */
        if( ( SYSTEM_Init() == pdPASS ) && ( xTasksAlreadyCreated == pdFALSE ) )
        {
            /* Run all demos. */
            DEMO_RUNNER_RunDemos();
            xTasksAlreadyCreated = pdTRUE;
        }
　　　
　　<<ここまででリンク通った>>
　　
　　　ダウンロードして実行してみる。
　　　従来通り、ルネサスTCP/IPが起動し、無事DHCPでIPアドレス取得できている。
　　　FreeRTOS+TCPを入れたことで、従来の動作(主にEtherドライバ部分)に影響ないことを確認。
　　　これから、main付近(rx65n_envision_kit_aws.c)を改造し、ルネサスTCP/IPの初期化部分を
　　　除外していき、代わりにFreeRTOS+TCPno初期化部分を入れていく。
　　　
　　　configPRINTF()を有効にするため、FreeRTOS.hの以下を変更
　　　	#define configPRINTF( X )
　　　	↓
　　　	#define configPRINTF( X ) printf X
　　　	
　　　FreeRTOS_debug_printf()を有効にするため、FreeRTOSIPConfig.hの以下を変更
　　　	#define ipconfigHAS_DEBUG_PRINTF    0
　　　	↓
　　　	#define ipconfigHAS_DEBUG_PRINTF    1
　　　	
　　　RX65Nの今回のシステムはprintf()出力を液晶表示に繋いであるので、
　　　これでFreeRTOS関連のシステムログが液晶表示に出てくるはず。
　　　
　　　PICのコードを見ると、FreeRTOS_IPInit()を呼び出せばTCP/IPの初期化が走るようだ。
　　　FreeRTOS_IPInit()の実装体を確認する。
　　　第1～第4引数はIP関連のパラメータ。DHCP有効であれば自動取得するはずなので設定不要。
　　　第5引数のMACアドレスは入力必要であろう。適当にMACアドレスの配列を作って入力する。
      FreeRTOS_IPInit(0, 0, 0, 0, renesas_mac_address);
      このときのmain()は以下のように実装。

void main(void)
{
	char buff[256];

	R_Pins_Create();
	R_SYS_TIME_Open();
	lcd_open();
	R_SIMPLE_GRAPHIC_Open();

	/* hello message */
	sprintf(buff, "hello, this is RX65N Envision Kit system log.\r\n");
	printf("%s", buff);
	sprintf(buff, "built in %s, %s\r\n", __DATE__, __TIME__);
	printf("%s", buff);
	sprintf(buff, "\r\n");
	printf("%s", buff);

    	FreeRTOS_IPInit(0, 0, 0, 0, renesas_mac_address);
}

　　　FreeRTOS_IPInit()終了後、IPタスクが起動して、prvIPTask()は呼ばれたようだ。
　　　eNetworkDownEventのprvProcessNetworkDownEvent()が呼ばれたところで暴走。
　　　詳細を追いかけていく。
　　　
　　　xNetworkInterfaceInitialise()が呼ばれるが初期化関数が無い状態。
　　　ひとまずlan_open()を呼んでおく。xNetworkInterfaceInitialise()としては
　　　戻り値は 1(pdTRUE) が成功のようだが、lan_open()は成功時 0 が戻るので調整しておく。
　　　RXマイコンのEtherは、LANケーブル挿抜の状態を確認するため、R_ETHER_LinkProcess()を定期的に
　　　呼び出す必要がある。FreeRTOSでタスクを生成して監視させれば良いが、
　　　まだFreeRTOSの使い方がよくわからないため、CMTを1チャネル消費して監視させる。(後で調べる)★→OK
　　　
　　　たぶん、LANケーブル挿抜のイベントをTCP/IP側に通知する仕組みがあるが、ひとまず、
　　　xNetworkInterfaceInitialise()が完了したときにリンクアップ完了しているように
　　　xNetworkInterfaceInitialise()内部で待つようにしておく。(後でちゃんと実装する)★
　　　
　　　暴走はなくなった。でもxNetworkInterfaceInitialise()が失敗したら常に暴走するのでは？(後で調べる)★→現状特に問題なし
　　　IPタスクのループが動き続けていることを確認。
　　　
　　　TCP/IP起動時はきっとDHCPが動くであろうから、DHCPの処理を追いかけていく。
　　　どこかでDHCPの初手である、DHCP Discover Packetの生成を行っていて、
　　　その後、ネットワーク層に送信するはずである。
　　　
　　　DHCPの送信の前に、そもそも送信受信用のバッファが適切に割り当てられていないはず。
　　　なぜなら、vNetworkInterfaceAllocateRAMToBuffers()が未実装だから。
　　　まずはこれを調整する。
　　　
　　　ポーティングガイドを見ると、ipconfigNUM_NETWORK_BUFFER_DESCRIPTORS で定義される分だけ、
　　　バッファを割り当てよ、と書いてある。検索すると、FreeRTOSIPConfig.hに60と定義されている。
　　　おそらくここで割り当てるべきは送信バッファのみと思われる。(本当か？）★→送信バッファではなく受信バッファ。
　　　RXマイコンのEtherの実際の送信バッファ数は、r_ether_rx_config.hのETHER_CFG_EMAC_TX_DESCRIPTORSで定義される。
　　　60の代わりに、これを読み込んでおく。
　　　
　　　ETHER_CFG_EMAC_TX_DESCRIPTORSがデフォルト1だけれど、1のままだと暴走する。
　　　4に増やす。ETHER_CFG_EMAC_RX_DESCRIPTORSも4に増やす。(なぜか？）★→1でも大丈夫になった。
　　　
　　　vNetworkInterfaceAllocateRAMToBuffers()の実装体は、Etherドライバにおける
　　　送信バッファのポインタをFreeRTOS+TCPに渡すように実装する。
　　　
　　　vDHCPProcess()を内部に進む。
　　　　中身は伝統的なswitch-caseのステートマシンである。
　　　　予想通り、最初の状態にdiscover requestの送信があった。
　　　　/* Send the first discover request. */
　　　　prvSendDHCPDiscover()に潜っていく。
　　　　　正常に送信リクエストが出ているようだが、vApplicationStackOverflowHook()で停止する。
　　　
　　　r_bsp_config.hでスタックを増やしてみる。FreeRTOSはユーザスタックも使用するようだ。
　　　　#pragma stacksize si=0x400
　　　　↓
　　　　#pragma stacksize si=0x2000

　　　　#pragma stacksize su=0x1000
　　　　↓
　　　　#pragma stacksize su=0x2000

　　　スタック周りを触っていたら、何度かIPタスクのループを
　　　実行したところで暴走するようになってしまった。元にも戻せなくなった。
　　　(動いている状態をバックアップしておけばよかった）
　　　
　　　今日はここで終わり！

--------------------------------------------------------------------------
2018/02/14
rx65n_rsk_awsで作業開始。
FreeRTOSの 8.2.2のコードを結合していく。

FreeRTOS内のport.cに #include "iodefine.h"があったので、 
#include "platform.h" に変更

\rx65n_rsk_aws\src\amazon-freertos-master\lib\FreeRTOS\Source\portable\MemMangの
heap_3.c と heap_4.c が両方ビルド対象になっているが、heap_4.c のみが適切。
何でそうなのかは知らない。　（なんでか後で調べる）

インクルードファイルパスの調整などを経て 8.2.2の環境で動作確認完了。
FreeRTOSのコードを 9.0.0に変更し動作確認完了。
FreeRTOSのコードを 11.0.0に変更し動作確認完了。

rx65n_envision_kitにボード非依存部分のコードを移植し動作確認。問題なし。

--------------------------------------------------------------------------
2018/02/12
コード調整再開。

先ず作戦を考える。NoMaY氏は上位レイヤーからの調整を実施しているので、
私は下位レイヤーから積み上げていき、良いタイミングでマージするのが良い。
NoMaY氏の活動をみると大きく4点ステップがありそう。
①FreeRTOSで動作させる
②FreeRTOS+TCPを動作させる
③mbed TLSを動作させる
④実際にAWSに繋ぐ

先ずは①を対応するため、RX65N用に用意されたOSパッケージを参考にする。
https://www.renesas.com/en-us/software/D6001925.html

この中には、特殊なFITモジュールが入っていることはNoMaY氏の調査により確認済み。
r_bsp_rtos
r_cmt_rtos

これを(2017/12/29)のものに含まれる以下2点と置き換えてやれば
FreeRTOSと結合できるのではないか。
r_bsp
r_cmt_rx

diffをとって、クリティカルなところを(2017/12/29)に反映していく。

(1)r_bsp の resetprg.c でOS用のインクルードファイルを呼んでるところ
#if BSP_CFG_RTOS_USED == 0      // Non-OS
#elif BSP_CFG_RTOS_USED == 1    // FreeRTOS
    #include    "freertos_usr_func.h"    // FreeRTOS's user configuration
#elif BSP_CFG_RTOS_USED == 2    // SEGGER embOS
#elif BSP_CFG_RTOS_USED == 3    // Micrium MicroC/OS
#elif BSP_CFG_RTOS_USED == 4    // Renesas RI600V4 & RI600PX
#endif

(2) r_bsp の resetprg.c と r_cmt_rx の r_cmt_rx.c において、
　上記マクロに伴いFreeRTOS用のコード各所
　（カーネルのスケジューラを呼び出しているところなど）も反映。

(3) r_bsp の r_bsp.h にFreeRTOSのヘッダファイル群のインクルードを追加。
　ユーザからはRXマイコンのFIT群のヘッダファイルplatform.h をインクルード
　すればよいようになる。

#if BSP_CFG_RTOS_USED == 0      // Non-OS
#elif BSP_CFG_RTOS_USED == 1    // FreeRTOS
#include "FreeRTOS.h"
#include "task.h"
#include "semphr.h"
#include "queue.h"
#include "croutine.h"
#include "timers.h"
#include "event_groups.h"
#elif BSP_CFG_RTOS_USED == 2    // SEGGER embOS
#elif BSP_CFG_RTOS_USED == 3    // Micrium MicroC/OS
#elif BSP_CFG_RTOS_USED == 4    // Renesas RI600V4 & RI600PX
#endif

(3)BSPのコンフィグ(r_bsp_config.h)にあるリアルタイムOS切り替えの
　マクロ(BSP_CFG_RTOS_USED)でFreeRTOSを選択する。
　すると、(2)で反映した部分のFreeRTOS関連のコードが有効になる。
　FreeRTOSに対応するマクロ番号は(1)。
　デフォルトの(0)だとRTOSを使わない設定となる。

(4)BSPのコンフィグ(r_bsp_config.h)にあるタイマチャネルの指定について以下追加。
/* This macro is used to select which CMT channel used for system timer of RTOS.
 * The setting of this macro is only valid if the macro BSP_CFG_RTOS_USED is set to a value other than 0. */
#if (BSP_CFG_RTOS_USED != 0)
/* Setting value.
 * 0      = CMT channel 0 used for system timer of RTOS (recommended to be used for RTOS).
 * 1      = CMT channel 1 used for system timer of RTOS.
 * 2      = CMT channel 2 used for system timer of RTOS.
 * 3      = CMT channel 3 used for system timer of RTOS.
 * Others = Invalid. */
#define BSP_CFG_RTOS_SYSTEM_TIMER		(0)
#endif

さて、次に使用するFreeRTOSのバージョン。
私が動作確認したことがあるのは8.2.2で、上記RX65N用に用意された
OSパッケージは9.0.0で、Amazon FreeRTOSは11.0.0である。
ひとまず、8.2.2を持ってきて、差分を埋めていく感じで進める。

協力会社と連携するため、ボードをRX65N RSKに乗り換え。
以降、rx65n_rsk_aws フォルダに移動。

--------------------------------------------------------------------------
2018/02/09
諸事情により開発一時停止。

--------------------------------------------------------------------------
2017/12/29 
RX65N Envision Kitを素材にする。
購入時はLANコネクタとSDスロットなどが付いてないので増設が必要。
先ずはe2 studio のスマートコンフィグレータ機能で
以下モジュールをインポートする。
- r_bsp
- r_cmt_rx
- r_ether_rx
- r_sys_time_rx
- r_t4_rx
- r_t4_driver_rx

⇒これでEther関連の動作確認ができる。
　端子設定はRX65N Envision Kitのコードと等しいかどうか調べながら調整。
　同じにすればEther関連は動くはず。
- r_pincfg

FITモジュール以外の以下ソースコードはRX65N Envision Kitのコードから流用する。
- lcd_conf.c
- r_ascii.c
- r_ascii.h
- r_simple_graphic.c
- r_simple_graphic_if.h

⇒これでprintf()でRX65N Envision Kitの液晶に文字表示が可能。
　システムログを画面に出す。
　ポーティングが進めば、SeggerのGUIも載せてウィンドウ形式にしたい。

ここまでの動作確認でPCからpingが通ることを確認した。

