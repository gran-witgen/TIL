### Hadoop

大規模なデータの処理、解析を実現するオープンソースウェア  

特徴  

- サーバ追加でスケーラビリティを実現
- スキーマ定義の不要
- 耐障害、故障

hadoopの構成は以下

- HDFS(hadoop dispersion　file system) hadoop分散ファイルシステム
- hadoop mapreduce 分散処理フレーム


- HDFS
マスタのNameNodeとスレイブのDataNodeにわかれる。

マスタはスレイブを管理、スレイブはデータの実体を保存する。

HDFSにデータを保存する場合、一定量のデータサイズのデータをブロックとして扱い、保存。

スレイブが壊れてもデータが欠損しないよう、ブロックを複数のスレイブにレプリカとして保存する。

RAID5のパリティみたいなもの？

- map reduce

map reduceを構成する二つのコンポーネント

- hadoop mapreduce処理基盤
- mapreduceアプリケーション

- hadoop mapreduce処理基盤
マスタノードであるJobTrackerとスレーブのTaskTrackerで構成。

マスタはスレーブのジョブ管理、タスク割り当て、リソース管理を行う。

スレーブが故障し、該当スレーブが処理していたタスクが実行されない場合もマスタが別のスレーブへタスクを割り当てることで

ジョブの遅延が発生しないような仕組みになっている。


- mapreduceアプリケーション

以下の役割がある。

- map処理  
- reduce処理  
- mapreduceジョブ定義  


- map処理  
入力データに対してキーバリュー形式にする。Pythonの辞書と同じにする

- reduce処理  
map処理のキー毎に集約されたデータに対し、処理を行う

- mapreduceジョブ定義  
map処理とreduce処理を処理するための情報を定義する


キーバリューで表されたデータに対し、キー毎にデータを集約する。

```python
result_dict: dict = {
    "key_1":
        [data1, data4, data8, data10],
    "key_2":
         [data2, data5, data6],
    "key_3":
         [data9, data13]
    }
```

上記のような形になるんかな
