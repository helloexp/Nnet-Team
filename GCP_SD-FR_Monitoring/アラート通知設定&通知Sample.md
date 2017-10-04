
### アラート通知設定

[アラート ポリシーを作成する際に利用できる通知オプションの一覧](https://cloud.google.com/monitoring/support/notification-options)
* SMS アラートの構成
* Google Cloud Console （携帯アプリ）の使用
* PagerDuty との統合
* Webhook の構成
* 通知に関する SNS の構成
* HipChat との統合
* Campfire との統合
* Slack との統合
<br><br>

■ 社内向けの通知アラートメールSample：
<br><br>

&#x1F534; 検知アラートメール：

件名：[ALERT] Metric Threshold on Instance (GCE) instance-1 on nnet-frgcp-projects instance-1<br>

Stackdriver has detected that one of your resources has entered an alert state.<br> 
Summary: CPU utilization for nnet-frgcp-projects instance-1 is above the threshold of 1 with a value of 1.603206.<br>
Violation Began: 2017-10-02 07:50:47 UTC (2 mins 4 secs)<br>
Condition Name: Metric Threshold on Instance (GCE) instance-1<br> 

View violation details:<br> https://app.google.stackdriver.com/incidents/0.ki2tfd8gpn0r?project=nnet-frgcp-projects 

&#x1F535; 復旧メール：

件名：[RESOLVED] Metric Threshold on Instance (GCE) instance-1 on nnet-frgcp-projects instance-1<br>

Stackdriver has detected that one of your resources has recovered.<br> 
Summary: CPU utilization for nnet-frgcp-projects instance-1 returned to normal with a value of 0.969576.<br> 
Violation Began: 2017-10-01 02:39:47 UTC (1 day 5 hours)<br> 
Condition Name: Metric Threshold on Instance (GCE) instance-1<br> 
Violation Lasted: 1 day 5 hours<br> 

View violation details:<br> https://app.google.stackdriver.com/incidents/0.ki18fnxzrm8m?project=nnet-frgcp-projects 
<br><br>

■ Slackチャンネル向けの通知アラートSample：

&#x1F534; 検知アラート通知： 

Google Cloud Monitoring APP [10:38 PM]<br> 
Incident #0.khxhrhntjyu5 started<br>
logging/user/nnet-gcp-apache for nnet-frgcp-projects instance-1 with metric labels {log=apache-error} is above the threshold of 1 with a value of 1.5166666666666666.<br> https://app.google.stackdriver.com/incidents/0.khxhrhntjyu5?project=nnet-frgcp-projects

&#x1F535; 復旧通知：

Google Cloud Monitoring APP　[10:39]<br> 
Incident #0.khxhrhntjyu5 resolved<br>
logging/user/nnet-gcp-apache for nnet-frgcp-projects instance-1 with metric labels {log=apache-error} returned to normal with a value of 0.25.<br> https://app.google.stackdriver.com/incidents/0.khxhrhntjyu5?project=nnet-frgcp-projects


