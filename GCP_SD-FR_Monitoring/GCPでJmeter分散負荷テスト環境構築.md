## GCPでJmeter分散負荷テスト環境構築                   

目的：<br>
GCPのAutoscale機能を利用し、試験必要なときのみJmeterSlaveサーバを自動作成し、Masterへの登録も自動化させる。<br>

構成：<br>
■ Masterコントローラ ：　Windows2016 64bit 1台<br>
■ Slaveサーバ       ： Centos-7 Autoscaleグループ<br>

手順：
### 1. Master:(terraform用)
   ■ Windows server 2016 Instance:<br>
   fr-dev-jmetermaster-windows-server2016

   インストール:(Slaveと同じバージョン）<br>
   。Jmeter binary zip file ダウンロードし、/apache-jmeter配下配置 (on server)<br>
   。Javaのインストール<br>
   。Powershellインストール(default)

   * Login to Jmeter master by RDP (Windows server)<br>
   User/Password: administrator/

### 2. Slaveサーバ作成用AMI構築(terraform用)
   * 1).インストール:(Masterと同じバージョン）<br>
   。Jmeter binary zip file ダウンロードし、/apache-jmeter配下配置 (on server)<br>
   。Javaのインストール<br>

   * 2).システムパラメータチューニング<br>
    /etc/security/limits.confに追加<br>
       root soft nofile 65535<br>
       root hard nofile 65535<br>

   * 3).jmeterブート時自動起動
     /etc/rc.localに以下を設定：<br>
     #rmiサーバ設定（java.rmi.server.hostname＝自身のPrivateIP)<br>
   PIV_IP=$(ifconfig eth0 | grep "inet " | awk '{print $2}' | awk -F ':' "{print $2}”)<br>
   sed -i -e "s/^RMI_HOST_DEF=-Djava.rmi.server.hostname=.*/RMI_HOST_DEF=-Djava.rmi.server.hostname=${PIV_IP}/" /home/mdhaque_israfil/src/apache-jmeter-2.9/bin/jmeter-server<br>
   /bin/bash -l /home/mdhaque_israfil/src/apache-jmeter-2.9/bin/jmeter-server & 

### 3.AMIからTemplate作成

### 4.TemplateからAutoscaleグループ作成
   Instance名:fr-dev-sandbox-jmeterslave-asg(1〜4)

### 5.GCPを利用してJmeterSlaveサーバのIP一覧を取得し、Jmeterの設定ファイルに自動設定<br>
* Powershellスクリプト作成:<br> 
    1). バッチファイル実行してからPowerShellを呼び出す<br>
　　　スクリプト名:set-jmeter-slaves.ps1<br>
　　　バッチファイル名:set-jmeter-slaves.bat

### 6.GCPを利用してJmeterMasterからUpload CSV file to JmeterSlaveの設定ファイルに自動設定
   * CSVファイルUploadのためPowershellスクリプト作成：<br>
   1). バッチファイル実行してからPowerShellを呼び出す<br>
　　　  スクリプト名:upload_jmeter_csv_files.ps1<br>
　　　  バッチファイル名:upload_jmeter_csv_files.bat

### 7.jmeter bat fileを実行する：on Windows Master server
* 1).apache-jmeter-2.9\ae-jmeter-2.9\bin\<br>
      click "jmeter.bat" <br>
    スクリプト名:upload_jmeter_csv_files.ps1<br>
     .jmeterでテストのため設定する：<br>
    1). スレッドグループを追加<br>
    2). HTTP リクエストサンプラーを追加設定<br>
    3). 結果をツリーで表示リスナーを追加<br>
    4). 結果をツリーで表示を設定<br>
    5). テストを実行<br>
    6). テストの実行結果を確認<br>

### 8.jmeter server fileを実行する：on Centos-7 Slave server
* 1).apache-jmeter-2.9/ae-jmeter-2.9/bin/jmeter-server
​        



