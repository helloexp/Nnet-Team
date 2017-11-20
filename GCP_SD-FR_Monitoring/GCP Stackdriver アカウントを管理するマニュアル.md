### GCP Stackdriver アカウントを管理するマニュアル

目次

1. Stackdriverアカウントの作成
2. エージェントのインストール
3. 稼働時間チェックとアラート ポリシーの作成
4. ダッシュボードとグラフの作成
5. ログを見る
6. クリーンアップ

### 1. Stackdriverアカウントの作成

■ プロジェクトは Stackdriver にある必要がある為アカウントを作成方法

　　1. Cloud Platform Console で、[Stackdriver] > [監視] を選択する。<br>
　　2. プロジェクトが Stackdriver<br> アカウントにないため、次のメッセージが表示される。<br>
　　![](create%20a%20new%20account.png)<br>
　
    3. [Create new Stackdriver account]<br> をクリックし、次に [続行] をクリックすると以下のページが表示される。
    ![](create-a-stackdriver-account.png)<br>
　　4. 自分の「Project Name」プロジェクトが表示されたら、[Create account] をクリックする。<br>
　　5. [Add Google Cloud Platform projects to monitor] ページで、[Continue] をクリックしてスキップする。<br>
　　6. [Monitor AWS accounts] ページで、[Done] をクリックしてスキップする。<br>
　　7. 数秒で、次のメッセージが表示される。<br>
　　![](finished-initial-collection.png)<br>[Launch Monitoring] をクリックする。<br>
　　8. [Get reports by email] ページで、[No reports]、[Continue] の順にクリックする。<br>
　　9. Stackdriver アカウントのダッシュボードが表示される、必要でない場合は、「Welcome to Stackdriver」バナーを閉じます。
    

### 2. Stackdriver エージェントのインストール
------

■ インスタンスでStackdriver エージェントのインストール下記のLinkから手順参照して、Stackdriver Monitoring と Logging エージェントをインストールする。<br>
[GCP_Stackdriverエージェントインストール手順](https://github.com/fastretailing/fr-monitoring-doc/blob/master/Service/GCP_SD-FR_Monitoring/GCP_Stackdriver%E3%82%A8%E3%83%BC%E3%82%B8%E3%82%A7%E3%83%B3%E3%83%88%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%89%8B%E9%A0%86.md)

### 3. 稼働時間チェックとアラート ポリシーの作成
---------

■ 稼働時間チェックは、ウェブサーバーが常にアクセス可能であることを確認するまた、アラート ポリシーは、稼働時間チェックが失敗した場合に誰に通知されるかを管理する。

　1. Stackdriver Monitoring Console へ戻る。<br>
　2. ダッシュボード上に、[Create an Uptime Check]<br> が表示されていたら、それをクリックする。表示されていない場合は、トップメニューで [Alerting] > [Uptime Checks]へ移動し、[Add Uptime Check] をクリックする。[New Uptime Check] パネルが表示される。<br>
　3. 稼働時間のチェックのために、次のフィールドに入力する。<br>
　　  ● Title: チェックの名前を入力する<br>
      ● Check type: HTTP、HTTPS、TCP<br>
    　● Resource Type: Instance、App Engine、Elastic Load Balancer、URL<br>
　　　● Applies To: Single、Instance Name選択<br>
　　　● 他のフィールドはデフォルト値のままにする。<br>
      ● Check every: 1、5、10、15 分のいずれか。
　　　● Advanced options（HTTP、HTTPS）
  4. [Test] をクリックして、稼働時間チェックが動作していることを確認する。<br><br>
   [稼働時間チェックを設定する方法について詳しく説明](https://cloud.google.com/monitoring/alerts/uptime-checks)<br><br>
　5. [Save] をクリックすると、<br>
　次のパネルが表示される。<br>
  ![](alerting-policy%20name.png)<br><br>
  6. 前のパネルで [Create Alerting Policy] をクリックします。次が表示される。<br>
　7. [Policy name] に「Instance のpolicy名」を入力する。<br>
  8. [Add notification] をクリックし、メールアドレスやSlack Channelsを記入する。<br>
　9. [Documentation] セクションに「Policyの条件やコメント」と入力する。<br>
　10. [Save Policy] をクリックする。

### 4. アラート ポリシー作成
------

■ アラート ポリシーを作成する。右側のメニュー内に[Create Alerting Policy]がある。<br>
条件チェックでStackdriverにアラートポリシーを作成することができる。

◎ [条件]:<br>
[Add condition]<br> をクリックし、下記の条件タイプ表示される:<br>
    ● Metric threshold: Opens an incident if a metric rises above or falls below a value for a specific duration window.<br>
    
※アラート ポリシーのトリガー
すべての条件違反がグループ内の単一のリソースで発生した場合にのみトリガーするポリシーを、作成することができる。<br>
「アラート ポリシーに 2 つ以上の条件を必要、そうでなければ、ポリシー トリガー オプションが示されません。」<br>
[Policy triggers] パネルで、[Criteria] を [All conditions are met] にセットし、右側のメニューから必要なオプションを選択する。<br>
    ● Metric absence: Opens an incident if a metric is unavailable (has no data) for a specific duration window.<br>
    ● Metric rate of change: Opens an incident if a metric increases or decreases by a specific percent or more during a duration window.<br>
    ● Uptime check health: Opens an incident if you've created an uptime check and the resource fails to successfully respond to a request sent from at least two geographic locations.<br>
    ● Process health: Opens an incident if the number of processes running on a VM instance or instance group falls above or below a specific number during a duration window.<br>
    
◎ [通知設定]:

アラート ポリシーを作成する際に利用できる通知オプションの一覧を以下に示するのでメールアドレスやSlack Channelsを記入する。<br>

◎ [Documentation]:

セクションに「Policyの条件やコメント」と入力する。<br>

◎ [Policy name] にのpolicy名」を入力する。<br>

◎ [Save Policy] をクリックする。


### 5. ダッシュボードとグラフの作成
------

■ Instancesのグラフやダッシュボード上で Stackdriver Monitoring が収集した指標を表示する:

  1. [Stackdriver Monitoring Console のトップメニューで、[Dashboards] > [Create] を選択する。<br>
  2. [Add Chart] をクリックします。[Add Chart] ページが表示される。<br>
  3. [Metric Type] メニューで、「監視設定したい項目」を選択する。プレビュー セクションにグラフデータが表示される。<br>
  4. [Save] をクリックする。<br>
  5. 2 つ目のグラフを作成する。新しいダッシュボードの右上で [Add Chart] を選択する。<br>
  6. 複数AddChart作成するときまた、[Metric Type] メニューで「他の監視項目」を選択する。<br>
  7. [Save] をクリックする。<br>
  8. 新しいダッシュボードで、[Untitled Dashboard] を「CreateしたStackdriver  dashboard」に変更する。


### 5. ログを見る
------

■ Stackdriver Monitoring Console のトップメニューで [Logs] をクリックする。ログビューアが表示される。ご希望のログを見るには、ログビューアのフォーカスを変更する。

　1. 最初のプルダウン メニューで、[Compute Engine] > [Instance] > [All resource IDs] を選択する。<br>
  2. ログメニューで [syslog] を選択する。<br>
  3. VM インスタンスからの syslog ログが表示される。<br>
  ![](logs-viewer.png)<br><br>
  4. Stackdriver Monitoring Console へ戻る。グラフの 1 つで設定メニューを開いて、[View Logs] を選択するとグラフに、時間スパンとデータに対応するログが表示される。 
    

### 6. クリーンアップ設定削除について
------

■ インスタンスをシャットダウンしたときにエラーが出ないように、Stackdriver グラフやアラートポリシーを削除する。<br>

　1. [Alerting] > [Policy Overview]からアラート ポリシーを削除する。<br>
  2. [Alerting] > [Uptime Checks]から稼働時間のチェックを削除する。<br>
  3. [Dashboards] > [Untitled Dashboard Name]から、グラフを削除する。
    

■ Compute Engine の VM インスタンスのページで VM インスタンスを開始や停止することできる。<br>
　　
　1. インスタンスを選択する。<br>
  2. ページの上部で、[開始]、[停止] または [削除] をクリックする。


■ 完全に削除するには、作成したプロジェクト、「stackdriver-Project-Name」を削除する。

----------------------------------




