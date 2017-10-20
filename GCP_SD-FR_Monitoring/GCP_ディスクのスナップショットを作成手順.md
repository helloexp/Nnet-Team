## Google Cloud Platform の ディスクのスナップショットを作成するドキュメント

###
【コンソール使用】:
###

■ スナップショットを作成する<br> 

1. [新しいスナップショットの作成] ページに移動する
2. スナップショットの名前を入力し、スナップショットを作成する既存のディスクを選択する
3. [作成] をクリックしてスナップショットを作成する

■ インスタンスにスナップショットから作成したディスクを追加する

    * スナップショットからディスクを作成してインスタンスに接続 

1. [VM インスタンス] ページに移動する
1. ディスクを追加するインスタンスの名前をクリックする
1. インスタンス詳細ページの一番上で [編集] をクリックする
1. [追加ディスク] の下で [項目を追加] をクリックする
1. 追加リストの [名前] 列で、[ディスクを選択し] プルダウン メニューをクリックして [ディスクの作成] を選択する
1. 新しいディスクのプロパティを構成し、ディスクの名前を指定して、[スナップショット] オプションを選択する
1. 対象のソースのスナップショットを選択する
1. [作成] をクリックしてディスクを作成する
1. インスタンス詳細ページの一番下で[保存]をクリックし、変更内容をインスタンスに適用して新しいディスクを接続する
1. 新しいディスクを作成してインスタンスに接続したら、ディスクをマウントする必要がある

■ インスタンスでは、接続したディスク上のシステム確認

1. [VM インスタンス] ページに移動する 
2. 新たにディスクを接続したディスクの横の [SSH] ボタンをクリックし、<br>
インスタンスに対する端末接続がブラウザに開く

#下記コマンドを使用して追加ディスクのファイルシステムを確認<br>
df -h<br>
lsblk

###
【GCLOUD使用】:
###

■ スナップショットを作成する<br> 

* Projectのブラウザに　[gcloud shell]　ボタンをクリックし、[SDK] に移動する

#Disksの一覧を表示するのコマンドを実行<br>
gcloud compute disks list

#Zoneの一覧を表示するのコマンドを実行
gcloud compute zones list

#disksからスナップショットを作成するには下記コマンドを実行<br>
gcloud compute disks snapshot [DISK_NAME] --snapshot-names=[SNAPSHOT_NAME] --zone=[ZONE]

#スナップショットの一覧を表示するのコマンドを実行<br>
gcloud compute snapshots list

#スナップショットについての情報を一覧表示するコマンドを実行<br>
gcloud compute snapshots describe [snapshot-name]

■ 作成したスナップショットからディスクを作成する<br>

#Diskを作成するには下記コマンドを実行<br>
gcloud compute disks create [DISK-name] --source-snapshot=[snapshot-name]

#Diskの一覧を表示するのコマンドを実行<br>
gcloud compute disks list

■ ディスクを作成してインスタンスに接続 

#Instanceの一覧を表示するのコマンドを実行<br>
gcloud compute instances list

#ディスクをインスタンスに接続<br>
gcloud compute instances attach-disk [INSTANCE-name] --disk=[DISK-name]

#下記コマンドを使用して追加ディスクのファイルシステムを確認<br>
gcloud compute ssh [INSTANCE-name]<br>
df -h<br>
lsblk

■ インスタンスでは、接続したディスク上のシステム確認

#下記コマンドを使用してDirectory作成し、追加ディスクをMountするのディスク&ファイルシステムを確認<br>
mkdir /mnt/disks<br>
mount /dev/sdb /mnt/disk

