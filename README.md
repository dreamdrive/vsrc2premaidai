# vsrc2premaidaiについて
VS-RC003(Vstone社製ロボット用制御ボード)をシリアルポート経由で接続し、gazebo(ROS)上のプリメイドAIをRobovieMaker2で制御するためのパッケージです。
PCが2台(Win & Ubuntu)必要で、PCとPCをマイコン経由で繋ぐという、かなり無駄の多い構成です。(^^;A
RobovieMaker2でROS上のロボットを動かせるというのは、珍しいと思います。

![ros2vsrc](http://dream-drive.net/images/robovie_ros.jpg "vsrc2premaidai")

## 準備するもの
- Vstone社 VS-RC003/HV基板 16,500円(ロボットショップ)
  - https://www.vstone.co.jp/robotshop/index.php?main_page=product_info&products_id=1761
- USBシリアル変換ケーブル(3.3V TTLのもの) 400円(Amazon)
  - https://www.amazon.co.jp/dp/B00K7YYFNM/ref=cm_sw_em_r_mt_dp_E2QmFbV1NJ0N9
- Robovie-Maker2がインストールされたWindows PC
  - https://www.vstone.co.jp/products/vs_rc003hv/download.html
- ROSがインストールされたUbuntu PC (18.04 & Melodic / gazeboが動くスペック)
  - http://wiki.ros.org/ja
- chikutaさんのプリメイドAIパッケージ各種インストール
  - https://github.com/chikuta/premaidai_description
  - https://github.com/chikuta/premaidai_controller
  - https://github.com/chikuta/premaidai_simulator

# 使い方

## 事前準備

1. UbuntuPCへのROS(Melodic)のインストールおよび、chikutaさんのプリメイドAIパッケージ各種は事前にインストールを済ませてください。
2. 本パッケージ(vsrc2premaidai)は、WindowsPCおよびUbuntuPC、どちらにもcloneしてください。

## RobovieMaker2とVS-RC003の初期化および設定

1. vsrc_premaidai/ai.rpjをRobovieMaker2で開きます。
2. VS-RC003を初期化したうえで、[プロジェクトの設定]→[CPUの設定]を選択します。
3. [CPUの設定]より、[基本設定]の[CPU基本制御周期]を"10000usec"に変更します。
4. [CPUの設定]より、[シリアル設定]の[CN6]を"コマンドポート"に変更します。
5. [モードスイッチ]より、CPUへの書き込みを実行します。


## VS-RC003とUbuntuPC(ROS)との接続(配線)

接続は、シリアル変換ケーブルを用いて接続します。
例のAmazonのケーブルの場合、
- VS-RC003 CN6-P1(TXD1) ← USB-TTLケーブル 白
- VS-RC003 CN6-P2(RXD1) ← USB-TTLケーブル 緑
- VS-RC003 CN6-P10(GND) ← USB-TTLケーブル 黒

USB/TTL変換ケーブルは、Ubuntu PCのUSB端子に接続します。

![ros2vsrc](http://dream-drive.net/images/connect_vsrc.jpg "connect_vsrc")

## 実行方法

1. WindowsPCとVS-RC003をUSBケーブルで繋ぎ、RobovieMaker2とVS-RC003を通信状態にします。
2. VS-RC003とUbuntuPCがUSBシリアル変換ケーブルで繋がっていることを確認します。
3. Ubuntu PCにて、下記launchを起動します。
```
$ roslaunch vsrc2premaidai vsrc_control.launch
```
4. gazebo上に、プリメイドAIが表示されたら、WindowsPC上のRobovieMaker2のスライダを動かしてください。gazeboのプリメイドAIが動けばOKです。

# 謝辞
プリメイドAIのROSパッケージを作ったchikutaさんと、解析した先人の皆さんに感謝です。

MIT License / Copyright (c) 2020 Hirokazu Onomichi
