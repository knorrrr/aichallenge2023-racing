# Local Environment
 &emsp;参加者の皆様にはシナリオを遂行するROS2パッケージを作成していただきますが、本リポジトリ内でそのベースとなるサンプルコードとしてaichallenge2023-racing/docker/aichallenge/aichallenge_ws/srcに以下のROS2パッケージを提供しております。  
 &emsp;作成していただいたROS2パッケージは、aichallenge_ws/src/aichallenge_submit以下に配置していただき、下記手順でビルド・実行できるようにしてください。
  
## Sample Code
 &emsp;aichallenge2023-racing/docker/aichallenge/aichallenge_ws/src配下の構成を一部示します。
* aichallenge_launch
  * 大元のlaunchファイルaichallenge.launch.xmlを含んでいます。すべてのROS2ノードはこのlaunchファイルから起動されます。
* aichallenge_scoring WIP
  * AI チャレンジの参加者のスコアリングとランキングに必要なタスクを担当します。
* aichallenge_scoring_msgs WIP
  * スコアリング用のmsg
* aichallenge_scoring_result WIP
  * /aichallenge/scoreと/aichallenge/collisionからスコアを算出します。
* aichallenge_submit
  * 提出時にはこのディレクトリの内容のみ提出していただきますので、参加者の皆さまが実装されたROS2パッケージはすべてこのディレクトリ内に配置してください。
  * aichallenge_submit_launch.launch.xmlが大元のlaunchファイルaichallenge.launch.xmlから呼び出されますので、このlaunchファイルを適宜改修して皆様が実装されたROS2ノードが起動されるように設定してください。
  * autoware_launch, autoware_universe_launch
    * Autowareのlaunch, config関連のパッケージをコピーして一部編集しています。Dockerイメージ内のAutowareにはここに含まれているパッケージが削除されています。こちらを編集することでAutowareの動作の変更を行うことが出来ます。
    * 改変前のファイルを利用したい場合は、[autoware_launch](https://github.com/autowarefoundation/autoware_launch/tree/awsim-stable), [autoware_universeのlaunchディレクトリ](https://github.com/autowarefoundation/autoware.universe/tree/awsim-stable/launch)をご利用ください。

### Steps for Execution
1. Docker Image Build
```
#aichallenge2023-racingディレクトリで
cd docker/train
bash build_docker.sh
```

2. Docker Container Run
GPU環境がある方は
```
#aichallenge2023-racingディレクトリで
cd docker/train
bash run_container.sh
```
CPUのみの環境の方は
```
#aichallenge2023-racingディレクトリで
cd docker/train
bash run_container_cpu.sh
```
1. Code Build
```
# Rockerコンテナ内で
cd /aichallenge
bash build_autoware.sh
```
1. AWSIMとAutowareの起動  
[Setupページ](../setup/index.html)を参考に起動。

 &emsp;セットアップが正常に行われていれば、rvizには地図が表示され、自動運転が開始されます。
 
 ### Customizing Autoware

 既存のAutowareをカスタマイズし、新しくパッケージを追加する方法等は夏の大会で使用した「[Customizing Autoware](../customize/index.html)」のページが参考になります．