# Raspberry pi Pico
組込み開発向けのマイコンボード
## Thonnyのダウンロード
Language: 日本語

Initial settings: Standard

[Thonny, Python IDE for beginners](https://thonny.org/)
## Picoセットアップ
ホームページからUF2ファイルをダウンロード。

[Getting Started with RP2040 – Raspberry Pi](https://www.raspberrypi.org/documentation/rp2040/getting-started/)

Pico上のBOOTSELボタンを押しながらmicroUSBを挿入。

Picoのフォルダー(RPI-RP2)にUF2ファイルを移動。

Thonnyを開く。実行→Select interpreter

コード: MicroPython (Raspberry Pi Pico)

Port: USBシリアルデバイス※複数あれば全て試す

Shellに`MicroPython v1.15 on 2021-04-18; Raspberry Pi Pico with RP2040`と出ればOK。

## 点灯/消灯
左上の緑色のボタンで実行
```
from machine import Pin

led = Pin(25, Pin.OUT)

led.toggle()
```

## 点滅
動作を止めるには赤色のSTOPボタンを押す。
```
from machine import Pin, Timer

led = Pin(25, Pin.OUT)
tim = Timer()
def tick(timer):
    global led
    led.toggle()

tim.init(freq=2.5, mode=Timer.PERIODIC, callback=tick)
```

参考

>[Getting Started with RP2040 – Raspberry Pi](https://www.raspberrypi.org/documentation/rp2040/getting-started/)

>[【ワンコイン】最新ラズパイ『Raspberry Pi Pico』で電子工作！遊び倒してみました！ - YouTube](https://www.youtube.com/watch?v=W7fyiWzF04o)

20210430

# Pico C/C++ 環境構築
ワークフォルダ名を`pico-hi`とする。

GitBash
```
mkdir  pico-hi && cd pico-hi
git init
git submodule add https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk && git submodule update --init && cd ..
touch CMakeLists.txt
cp pico-sdk/external/pico_sdk_import.cmake .
mkdir pj_base && cd pj_base
touch CMakeLists.txt Main.cpp
```
pico-hi/CMakeLists.txt
```
cmake_minimum_required(VERSION 3.12)

set(PICO_SDK_PATH ${CMAKE_CURRENT_LIST_DIR}/pico-sdk)
include(pico_sdk_import.cmake)

set(ProjectName "pico-work")
project(${ProjectName})
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_subdirectory(pj_base)
```
pico-hi/pj_base/CMakeLists.txt
```
set(BinName "pj_base")
add_executable(${BinName}
    Main.cpp
)

pico_enable_stdio_usb(${BinName} 1)
pico_enable_stdio_uart(${BinName} 1)

target_link_libraries(${BinName} pico_stdlib)
pico_add_extra_outputs(${BinName})
```
pico-hi/pj_base/Main.cpp
```
#include <cstdint>
#include <cstdio>

#include "pico/stdlib.h"

int main() {
    stdio_init_all();
    const uint32_t LED_PIN = 25;
    gpio_init(LED_PIN);
    gpio_set_dir(LED_PIN, GPIO_OUT);

    while (true) {
        printf("Hello, world!\n");
        gpio_put(LED_PIN, 1);
        sleep_ms(250);
        gpio_put(LED_PIN, 0);
        sleep_ms(250);
    }

    return 0;
}
```

参考
>[Raspberry Pi Pico C/C++ SDK 環境構築 on Windows 10 - Qiita](https://qiita.com/iwatake2222/items/33b4cd3a39da5a44dc02)

20210507

# Pico C/C++ 環境構築

↓これを見てくれ。

<a href="https://youtu.be/K0LNCunQZUw"><image src="images\youtube.png" width="200" alt="YouTube" style="margin: 0 auto;"></a>

## ARM GCC
最新版をインストール
>[GNU Toolchain | GNU Arm Embedded Toolchain Downloads – Arm Developer](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)

Add path to environment variableにチェック

## Git
最新版をインストール
>[Git - Gitのインストール](https://git-scm.com/book/ja/v2/%E4%BD%BF%E3%81%84%E5%A7%8B%E3%82%81%E3%82%8B-Git%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)

ドロップダウンメニューでUse NotePad++ as Git's default editerを選択

ラジオボタンでCheckout as-is ,comment as-isを選択

ラジオボタンでUse Windows' default console windowを選択

Enable experimental support for pseudo consoles.をチェック

## Python
Python3の最新版をインストール

Optional Featuresをすべてチェック

Advanced Options:
Associate files with Python (requies the py launcher)
create shortcuts for installed applications
Ad Python to environment variables
Precompile standard library をチェック

## CMAKE

Windows Source (has \r\n line feeds)最新版をインストール

>[Download | CMake](https://cmake.org/download/)

動画の通りシステム環境変数を追加

GitBash
pico-hi>
```
git clone -b https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init
cd ..
git clone -b master https://github.com/raspberrypi/pico-examples.git
```

## Visual Studio Build Tools
最新版をインストール
WordloadsでC++ build toolsにチェックを入れてインストール

(Visual Studio 2019 for Windows および Mac のダウンロード)[https://visualstudio.microsoft.com/ja/downloads/]

環境変数を設定
pico-hi >
```
setx PICO_SDK_PATH "..\..\pico-sdk"
```

Developer Command Prompt for VS 2019を開く
```
code
```
※デスクトップアイコンからVS Codeを開いてもダメ。

拡張CMake Toolsをインストール

Settings→Extensions

Cmake: Configure Environment
Item: `PICO_SDK`
Value: `..\..\pico-sdk`

Cmake: Generator
`NMake Makefiles`

右上のFile→Open Folder→pico-examplesを開く
下の青いフッターのbuildを選択
ドロップダウンメニューのGCC arm-none-eabiなんとかを選択
自動でビルドされる

参考
>[WindowsでのC/C++環境構築 ーRaspberry Pi Picoへの道2ー - Raspberry Pi - HomeMadeGarbage](https://homemadegarbage.com/pipico02)

20210514

# Pico
## Resetスイッチを取り付ける
RUN端子とGND間にタクト・スイッチをはんだ付けします。Resetボタンと呼ばれるようです。はんだ付けした反対側は接着剤で浮かないように留めます。

<a href="https://www.denshi.club/parts/2021/04/raspberry-pi-pico-2-42.html"><image src="images\resetswitch.png" width="400" alt="YouTube" style="margin: 0 auto;"></a>

>[Raspberry Pi Picoでプログラミング ② ラズパイ4の準備(2) 標準入出力の用意 | RaspberryPiクックブック](https://www.denshi.club/parts/2021/04/raspberry-pi-pico-2-42.html)

20210519

# C言語による文字出力
基本的にpico-examples/hello_world/usbフォルダのものを使用する。
serialフォルダのプログラムはおそらくGPIO1への出力である。

# CircuitPython
CircuitPythonのPicoのページから、UF2ファイルをダウンロード

>[Pico Download](https://circuitpython.org/board/raspberry_pi_pico/)

## キーボード操作
GithubのReleasesから一番新しいライブラリー（zipファイル）のダウンロード

>[Releases · adafruit/Adafruit_CircuitPython_HID](https://github.com/adafruit/Adafruit_CircuitPython_HID/releases)

zipファイルの中のlib/adafluit_hidをCIRCUITPY(:D)/libにコピペ

### Thonnyの設定
Thonnyを開くとエラーが出る。実行→Select interpreterからCircuitPython(generic)を選択

GithubのUsage exampleからこんな感じでThonnyにプログラムをコピペ

```python
import usb_hid
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keycode import Keycode

# Set up a keyboard device.
kbd = Keyboard(usb_hid.devices)

# Type lowercase 'a'. Presses the 'a' key and releases it.
kbd.send(Keycode.A)
```

上のプログラムを実行すると"a"が打たれる

>[adafruit/Adafruit_CircuitPython_HID: USB Human Interface Device drivers.](https://github.com/adafruit/Adafruit_CircuitPython_HID)

# Picoインターネット接続（未実行）
ネットワークモジュール
W5050
ENC28J60

(AliExpressが時間はかかるが安いかも)
※Wi-Fiを飛ばすときは技適に注意


>[Raspberry Pi PicoでNuttXを動かす - Qiita](https://qiita.com/yunkya2/items/55f1222e8b2b903dd7ff)

20210521

# PicoにOSをインストールする

## ほとんどはこれを見れば分かる
>[【NuttX】ラズパイPicoにOSをインストールしてみた！ - YouTube](https://www.youtube.com/watch?v=zz_Z2tBOVvI&t=320s)

Ubuntuでプロジェクトフォルダに移動し、Shellファイルをダウンロード&実行
```
wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
chmod +x pico_setup.sh
./pico_setup.sh
```
Githubから必要なパッケージをクローン
```
sudo apt install bison flex gettext libncurses5-dev gperf automake-1.15 libtool pkg-config
git clone https://github.com/apache/incubator-nuttx.git nuttx
git clone https://github.com/apache/incubator-nuttx-apps.git apps
git clone https://bitbucket.org/nuttx/tools.git
```
ディレクトリを移動して4つのコマンドを実行
```
cd tools/kconfig-frontends/
./configure --enable-mconf --disable-nconf --disable-gconf --disable-qconf
make
sudo make install
sudo /sbin/ldconfig
```

pico/nuttxに移動してビルド
```
cd ../../nuttx
./tools/configure.sh raspberrypi-pico:nsh
```

Pico送信側端子UART0 TXの番号を指定
```
make menuconfig
```

[0]UART0 configを使っているUART0 TX端子のGP番号(0 or 12 or 16 or 28)に指定してSAVE。EXIT 2回で閉じる。(GP番号：Pico裏面のGP～の番号)

viコマンドで.bashrc（設定ファイル）にパスを書き込む
```bash
vi ~/.bashrc
```
```
export PICO_SDK_PATH=/mnt/c/Users/川畑輝一/Documents/hitechlab/pico-hi/os/pico/pico-sdk
export PICO_EXAMPLES_PATH=/mnt/c/Users/川畑輝一/Documents/hitechlab/pico-hi/os/pico/pico-examples
export PICO_EXTRAS_PATH=/mnt/c/Users/川畑輝一/Documents/hitechlab/pico-hi/os/pico/pico-extras
export PICO_PLAYGROUND_PATH=/mnt/c/Users/川畑輝一/Documents/hitechlab/pico-hi/os/pico/pico-playground
```
Escボタンを押して、:wqコマンド入力&Enterで保存&終了
```vim
:wq
```
sourceコマンドで~/.bashrcを即座に反映
```bash
source ~/.bashrc
```

UF2ファイルを作成
```
make
```

PicoにUF2ファイルを移動。

___
## UART通信
現在はUSBを介したシリアル通信が出来ないので、PGIO端子上のUART端子で接続する。
UARTとは、Universal Asynchronous Receiver/Transmitterの頭文字をとった用語で、直訳すると汎用非同期式送受信機
>[UARTとは？シリアル通信に欠かせない集積回路を徹底解説！ | 半導体・電子部品とは | CoreContents](https://contents.zaikostore.com/semiconductor/4816/)

PicoのDocumentでUART通信ができるピンを選択。例えばGP1を出力（UART0 TX）、GP2を入力（UART0 RX）、GP3をGNDとして使う。

## Rasberry Piの設定
RasPiでGPIOシリアル接続ができるように設定しなければならない。
```
sudo raspi-config
```
Interface Options→Serial Portを選択。2つの質問に答える。<br>
Would you like a login shell to be accessible over serial? いいえ<br>
Would you like the port hardware to be enabled? はい<br>
finishして求められたら再起動。

## Raspberry Piとの接続
Documentの通りにRasPiとPicoを接続。

>[Getting started with Raspberry Pi Pico](https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf)

RasPiのターミナルでMinicomをインストールし、シリアル接続すればnshが出てくる。
```bash
sudo apt install minicom
minicom -b 115200 -o -D /dev/serial0
```

20210524

# COM PORT設定
`L:\tools\product-tools\USBシリアル各社ドライバ`から必要なドライバをインストール

# BAUD RATE(ボーレート)
Picoのボーレートは115200Hz

#define BAUD_RATE = 115200

20210629

# Pico モーションセンサー

モーションセンサーのピンの茶・赤・オレンジの順にPicoのVBUS・GP28・GNDに取り付ける。

<image src="images\motion_sensor_pin.jpg" width="300" style="margin: 0 auto;">

可変抵抗は、左が時間、右が感度。バランスはこのくらい。

<image src="images\motion_sensor_resistance.jpg" width="300" style="margin: 0 auto;">

Thonnyで以下のコードを実行。

```
import machine as m
import utime
from time import time
 
sensor = m.Pin(28, m.Pin.IN, m.Pin.PULL_DOWN) 
led = m.Pin(25, m.Pin.OUT)
led_red = m.Pin(11, m.Pin.OUT)

now = 0
pre = time()

def sensor_callback(Pin):
    global now
    global pre
    led.value(1)
    led_red.value(1)
    utime.sleep_ms(250)
    led.value(0)
    led_red.value(0)
    
    print("executed")
    
    now = time()
    print(now - pre)
    pre = now
         
sensor.irq(trigger = m.Pin.IRQ_RISING, handler = sensor_callback)


```

>[Raspberry Pi PicoをArduinoにしてモーションを検知してみる – スイッチサイエンス マガジン](https://mag.switch-science.com/2021/04/28/pir-with-arduino-raspberry-pi-pico/)

___

__Qustion__
