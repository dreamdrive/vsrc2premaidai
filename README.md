# vsrc2premaidaiについて
VS-RC003(Vstone社製ロボット用制御ボード)をシリアルポート経由で、ROS上のプリメイドAIのgazeboを制御するためのパッケージです。

準備するもの
- Vstone社 VS-RC003基板
- USBシリアル変換ケーブル(3.3V TTLのものが望ましい)
- Robovie-Maker2がインストールされたWindows PC
- ROSがインストールされたUbuntu PC (gazeboが)
- chikutaさんのプリメイドAIパッケージ

MIT License / Copyright (c) 2020 Hirokazu Onomichi

## vsrc_connect (ノード)
VS-RC003を制御するためのノードです。

* カスタムメッセージVsrcControlをSubscribします。  
VsrcControlはコントローラーのボタンの状態とトルクON/OFFの情報で構成され、Subscribした情報をもとにVS-RC003のメモリを書き換えます。
* VS-RC003の状態としてボードのメモリ上の情報を定期的にカスタムメッセージVsrcStateとBatteryStateへPublishします。  
接続先のノードから電源電圧やモーションの再生状況を監視するすることが出来ます。  
メッセージの詳しい内容は後記もしくは、msgファイルを参照してください。

## vsrc_control (サンプルノード)
公式joyパッケージのjoy_nodeからジョイスティックのトピック(/joy)をsubscribeし、VsrcControlのメッセージをpublishするサンプルノードです。
Xbox360のコントローラを例に作成しています。



# 使用例1 - PCにVS-RC003もジョイスティックも直接接続する場合

PCに接続した、XBOX360コントローラーをVS-RC003のコントローラーとして使用するサンプルlaunchです。シリアルポートのデバイス名をパラメータ"serialdev"にセットして起動してください。

```
$ roslaunch vsrc2premaidai vsrc_control.launch
```




# 謝辞
vsrc_connectの作成に至っては、こちらの記事を参考にさせていただきました。ありがとうございます。  
> https://qiita.com/srs/items/efaa8dc0a6d580c7c423
