### Google Cloud Platform の Stackdriverドキュメント

■ エージェントインストール手順

目次

1. 事前作業
2. Monitoring エージェントをインストール
3. Monitoring エージェント バージョンの決定
4. Logging エージェントをインストール
5. Logging エージェント バージョンの決定
6. モニタリング エージェントを承認確認
7. サードパーティ製アプリケーションの監視するエージェントを設定する方法
8. トラブルシューティング

### 1. 事前作業

* GCPプロジェクトの作成と設定を行う。<br>
* VM インスタンスを作成および設定を行う。<br>
* VM インスタンスにエージェントファイルをコピー。

### 2. Monitoring エージェントをインストール

■ モニタリング エージェントをインストールするには、VM インスタンス上で次のコマンドを実行しましょう。

#インストール スクリプトをダウンロード:<br>
curl -O https://repo.stackdriver.com/stack-install.sh

#次のコマンドでインストール スクリプトを実行<br>
sudo bash stack-install.sh --write-gcm

※ インストールの最後に、次のようなメッセージが表示されるはずです。<br>

Restarting services<br>
[ ok ] Restarting stackdriver-agent (via systemctl): stackdriver-agent.service.

#モニタリング エージェントを再起動実行コマンド<br>
sudo service stackdriver-agent restart

### 3. Monitoring エージェント バージョンの決定<br>

#インストール後正常に行なえているかエージェント バージョン確認<br>
sudo yum list stackdriver-agent

#エージェントを更新するには、次のコマンドを実行<br>
sudo yum update stackdriver-agent

#エージェントを削除するには、次のコマンドを実行<br>
sudo yum remove stackdriver-agent


### 4. Logging エージェントをインストール

■ Logging エージェントをインストールするには、次のコマンドを実行しましょう。

#インストール スクリプトをダウンロード:<br>
curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh

sha256sum install-logging-agent.sh<br>
#チェックサム コマンド sha256sum の出力は次のように確認する。<br>

8db836510cf65f3fba44a3d49265ed7932e731e7747c6163da1c06bf2063c301 <br> install-logging-agent.sh

#次のコマンドでインストール スクリプトを実行:<br>
sudo bash install-logging-agent.sh

#Logiingへ生成されていない必要なlog監視項目の「.conf」を下記に追加<br>
cd /etc/google-fluentd/config.d/

■ エージェントをテストする

#エージェントが実行されていることを確認:<br>
ps ax | grep fluentd

#コマンドを実行して、テスト メッセージを送信確認:<br>
logger "This is Some test message for log check"

※ ログビューアで、エージェントのテストログ エントリを確認。<br>

#エージェントを再起動コマンド実行<br>
sudo service google-fluentd reload<br>
sudo service google-fluentd restart

※ ロギング エージェントの再読み込みや再起動の後で、テスト メッセージを送信すること確認。

### 5. Logging エージェント バージョンの決定<br>

#エージェントのバージョン確認<br>
rpm -q google-fluentd

#エージェントをアップグレード:<br>
sudo yum upgrade google-fluentd

#上記のコマンドを実行しても、エージェントの設定ファイルが変更されることはありません。最新のエージェントとともにクリーンな設定ファイルを取得したい場合は、次のコマンドをインスタンス上で実行<br>
sudo yum upgrade google-fluentd google-fluentd-catch-all-config


#エージェントをアンインストールする場合:<br>
sudo service google-fluentd stop<br>
sudo yum remove google-fluentd google-fluentd-catch-all-config


### 6. モニタリング エージェントを承認確認

#Linux VM インスタンス上で、次のコマンドを実行<br>
curl --silent -f -H "Metadata-Flavor: Google" http://metadata.google.internal/computeMetadata/v1/instance/service-accounts/default/scopes<br>

※ [必要な承認範囲の 1つが表示された場合、正しい権限を持っていること。](https://cloud.google.com/monitoring/api/authentication#cloud_monitoring_scopes)

### 7. サードパーティ製アプリケーションの監視するエージェントを設定する方法

#VM インスタンス上で、GitHub の構成リポジトリから 監視プラグインをダウンロードし、ディレクトリ /opt/stackdriver/collectd/etc/collectd.d/ に置きます。<br>

#有効にする必要がある場合、ダウンロードした設定ファイルを編集してください。<br>
cd /opt/stackdriver/collectd/etc/collectd.d/ && curl -O https://raw.githubusercontent.com/Stackdriver/stackdriver-agent-service-configs/master/etc/collectd.d/アプリケーション.conf<br>

※  [アプリケーションの.conf 設定手順を参照Link](https://cloud.google.com/monitoring/agent/plugins/)

#設定ファイルを追加した後、エージェントを再起動コマンドを実行<br> 
sudo service stackdriver-agent restart

### 8. トラブルシューティング

■ [Monitoring エージェントのインストールで問題がある場合は、トラブルシューティング参照](https://cloud.google.com/monitoring/agent/install-agent)
<br><br>
■ [Logging エージェントのインストールで問題がある場合は、トラブルシューティング参照](https://cloud.google.com/logging/docs/agent/installation)


