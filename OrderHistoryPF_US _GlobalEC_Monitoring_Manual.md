
## OrderHistoryPF_US_GlobalEC_Monitoring_Manual

## Contents

1. Specific Remarks<br> 
2. Server List<br>
3. Operation Procedure<br>
4. How to Restart the Server<br>
5. Emergency Contact<br>

## 1. Specific Remarks

---------------------------------
  * Point of notes when delete monitoring   
     * Dont forget delete on Munin setup
     * When you contact regarding the deleted server, if there is detected alert, no need to action event, you can close about this case.<br>

----

The following settings are necessary to browser of each Server and Nagios server at this project.<br>

 * Require to VPN connection for FR project.

You are notified to customers via slack when alert occurs in all new infra projects, but if you receive a large amount of alerts then there may be need to inquiries to customers.

## 2. Server List
----

Monitoring Server: mnt01-a-vir-dxc-nagios-common ※To connect via the platform of step Server
----
| Type | Server Name | Local IP | PASSWD | Remarks |
| :-------:|:-------:|:-------:|:--------:|:-------:|
|EC2|mnt01-a-vir-dxc-nagios-common|10.177.211.247|PASSWD|Monitoring server|	
|EC2|us-east-1_orderhistory_EC2_prd11-b-vir-adminapp-orderhistory-fr|10.177.20.101|PASSWD|-|	
|EC2|us-east-1_orderhistory_EC2_prd01-b-vir-jenkins-orderhistory-fr|10.177.21.27|PASSWD|-|
|EC2|us-east-1_orderhistory_EC2_prd11-b-vir-syncapi-orderhistory-fr|10.177.23.34|PASSWD|-|
|EC2|us-east-1_orderhistory_EC2_zipapi-orderhistory-fr-asg【IP】|-|PASSWD|AutoScaling Server|
|EC2|us-east-1_orderhistory_EC2_nodejsapi-orderhistory-fr-asg【IP】|-|PASSWD|AutoScaling Server|
|EC2|us-east-1_orderhistory_EC2_indexingapi-orderhistory-fr-asg【IP】|-|PASSWD|AutoScaling Server|
|EC2|us-east-1_orderhistory_EC2_importer-orderhistory-fr-asg【IP】|-|PASSWD|AutoScaling Server|
|ELB|us-east-1_orderhistory_ELB_prd01-vir-importer-odhst-1830398214.us-east-1.elb.amazonaws.com|-|-|-|	
|ELB|us-east-1_orderhistory_ELB_prd11-vir-adminapp-odhst-1164701055.us-east-1.elb.amazonaws.com|-|-|-|	
|ELB|us-east-1_orderhistory_ELB_prd11-vir-api-odhst-1756127701.us-east-1.elb.amazonaws.com|-|-|-|
|ELB|us-east-1_orderhistory_ELB_prd11-vir-indexapi-odhst-1992937238.us-east-1.elb.amazonaws.com|-|-|-|
|ELB|us-east-1_orderhistory_ELB_prd11-vir-zipapi-odhst-1951925892.us-east-1.elb.amazonaws.com|-|-|-|
|DynamoDB|us-east-1_orderhistory_DynamoDB_prd11-vir-delete-order-orderhistory-fr|-|-|-|
|DynamoDB|us-east-1_orderhistory_DynamoDB_prd11-vir-order-transaction-orderhistory-fr|-|-|-|
|DynamoDB|us-east-1_orderhistory_DynamoDB_prd11-vir-sns-monitor-orderhistory-fr|-|-|-|
|SNS|us-east-1_orderhistory_SNS_prd01-tky-us-notification-orderhistory-fr|-|-|-|
|SNS|us-east-1_orderhistory_SNS_prd01-tky-us-zip-orderhistory-fr|-|-|-|
|SNS|us-east-1_orderhistory_SNS_prd11-tky-us-importer-catalog-notification-orderhistory-fr|-|-|-|
|SNS|us-east-1_orderhistory_SNS_prd11-tky-us-importer-ec-notification-orderhistory-fr|-|-|-|
|SNS|us-east-1_orderhistory_SNS_prd11-vir-unprocessed-notification-orderhistory-fr|-|-|-|
|SQS|us-east-1_orderhistory_SQS_prd01-vir-notification-orderhistory-fr|-|-|-|
|SQS|us-east-1_orderhistory_SQS_prd11-vir-notification-orderhistory-fr|-|-|-|
|Elastic Search|us-east-1_orderhistory_ElasticSearch_prd11-vir-es-orderhistory-fr|-|-|-|
|Beanstalk|us-east-1_orderhistory_Beanstalk_prd11-vir-worker-orderhistory-fr|-|-|-|

#### nrpe Command:

* nrpe Restart Command (※ command execute the following in below command from the monitoring server)
  /home/nnet/script/remote_nrpe_restart IP Address<br>
    「-i option OK? [n]: 」to display, Type a [y] and enter ※after execute this command、it will take some times.<br>
    「-i option OK? [n]: 」to display, if type a [n] then becomes cancel from this command.

* nrpe Start Command<br>
/home/nnet/nrpe/src/nrpe -d /home/nnet/nrpe/nrpe.cfg

Sample event of after execute this command:<br> #/home/nnet/script/remote_nrpe_restart {Target IP}

[root@mnt01-a-tky-nagios-common script]# /home/nnet/script/remote_nrpe_restart 10.184.232.11
-i option OK? [n]: y

PLAY [all] ******************************************************************** 

GATHERING FACTS *************************************************************** 
ok: [10.184.232.11]

TASK: [init.nrpe copy] ******************************************************** 
ok: [10.184.232.11]

TASK: [pkill] ***************************************************************** 
changed: [10.184.232.11]

TASK: [nrpe restart] ********************************************************** 
changed: [10.184.232.11]

TASK: [chkconfig control] ***************************************************** 
changed: [10.184.232.11]

PLAY RECAP ******************************************************************** 
10.184.232.11              : ok=5    changed=3    unreachable=0    failed=0

## 3. Operation Procedure
-----
Monitoring Server: mnt01-a-vir-dxc-nagios-common

■ ELB Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|BackendConnectionErrors<br>HTTPCode-5XX<br>HTTPCode-Backend-5XX<br>HealthyHostCount<br>UnHealthyHostCount|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email & phone contact|May_day|
|Latency|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|

■ EC2 Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|CPU-Utilization<br>DISK-/<br>Freeable-Memory<br>Swap-Usage|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact<br>※description of cause process is unnecessary to send by email|May_day|
|LOAD<br>iNode|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>※description of cause process is unnecessary to send by email<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact<br>※description of cause process is unnecessary to send by email|May_day|
|NTP-syncronization|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-CROND|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-MUNIN|No action required|/etc/rc.d/init.d/munin-node (stop/start/restart)|May_day|
|PROCS-SSH|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-SYSLOGD|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-LOGSTASH|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|LOG-boot|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/boot/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/boot.log<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/boot/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-cron|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/cron/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/cron<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/cron/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-messages|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>※Point of note③ Contact is unnecessary when detected the target log is the log related to "ldap"<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/messages/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/messages<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/messages/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-secure|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>※Point of note③ If there is a recent email of autoscale add, and if IP of the recent email matches the server IP of alert detection, then Ack is executed and not necessary to contact the client. After Ack executed and after recovery return to normal operation.<br>◇Sample of email title of autoscale add:<br>{Server Name} AutoScale server is added!<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/secure/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/secure<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/secure/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-spooler|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/spooler/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/spooler<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/spooler/NGWRD-file<br>※lock file is not generated|May_day|
|StatusCheckFailed-Instance|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|StatusCheckFailed-System|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-NodeJS|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|LOG-NodeJS|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/node/ANS-file<br>※ Check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>prd11-vir-indexingapi-orderhistory-fr<br>Log file<br>/var/log/fr/fr-order-indexer-api.log<br><br>prd11-vir-zipapi-orderhistory-fr<br>Log file<br>/var/log/fr/fr-order-zip-csv-extractor.log<br><br>prd11-vir-nodejsapi-orderhistory-fr<br>Log file<br>/var/log/fr/phase2/fr-order-api.log<br><br>prd01-vir-importer-orderhistory-fr<br>Log file<br>/var/log/fr/fr-us-importer-common.log<br><br>/var/log/fr/unhandled-exceptions.log<br><br>prd11-b-vir-syncapi-orderhistory-fr<br>Log file<br>/var/log/fr/fr-order-api.log<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/boot/NGWRD-file<br>※lock file is not generated|May_day|

■ DynamoDB Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|SystemErrors|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|May_day|

■ SNS Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|NumberOfNotificationsFailed|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|May_day|

■ SQS Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|SQS_ApproximateNumberOfMessagesDelayed|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|May_day|

■ Elastic Search Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|Domain Status|■ email contact:<br> When Domain Status alert was detected on prd11-vir-es-orderhistory-fr|Execute below this command<br>#/usr/local/nnetworks/nagios_ariake/script/check_es_state prd11-vir-es-orderhistory-fr|-|

■ Beanstalk Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|EB_STATUS|No action required|Check the value of health on the AWS management console window<br>If WARNING, no contact required<br>If CRITICAL, make phone contact<br>If its repeatedly detecting and recovering then contact to email<br>■ In case UNKNOWN status<br>① Contact email and escalate to person in charge of Specific Team<br>② If the UNKNOWN status is continues more than 30 minutes, then also escalate in charge of related Team.|May_Day|


## 4. How to Restart the Server
-----
##### Follow the instruction of the (AWS Management Console) server Restart Manual

Restart event is follow the "reboot" execute<br>
※Dont follow the stop/start  execute for restart event

If a case require to stop/start execute then escalate to related in-charge team and report current situation<br>

#### Check the following requires when executing the ELB detaching operation:<br>
 
1. Check and confirm the target server to remove from ELB on the AWS management console
2. Check access log of the server (/var/log/httpd/access_log),<br>
and Login each server to remove from ELB and confirm the access yes/no from the user.
3. If access is possible to execute of ELB detaching by the above procedure(2) then,<br>
Rollback ELB ⇒ Detaching operation is execute again

## 5. Emergency Contact Information
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and english template.
<br>
##### [By using Japanese and English mail Template]

■ Contact email address:

To: marutinandan.sharma@fastretailing.com, noritaka.hayama@fastretailing.com<br>
Cc: infra@mail.fastretailing.com   <br>

■ Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1|Hayama|080-3540-1829|	 


----------------------------------



