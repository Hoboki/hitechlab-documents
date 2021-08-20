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

