
## MobileApp Operation Manual

## Contents

1. Specific Remarks<br> 
2. Server List<br>
3. Operation Procedure<br>
4. How to Restart the Server<br>
5. Emergency Contact<br>
6. Submit to Troubleshooting Report

## 1. Specific Remarks

---------------------------------
  * Point of notes when delete monitoring   
     * Dont forget delete on Munin setup
     * When you contact regarding the deleted server, if there is detected alert, no need to action event, you can close about this case.<br>

----

The following settings are necessary to browser of each Server and Nagios at this project.<br>

 * Need to VPN connection for FR project.

You are notified to customers via slack when alert occurs in all new infra projects, but if you receive a large amount of alerts then there may be need to inquiries to customers.

※ Stop monitoring prohibited when the monitoring stops! Please be sure to turn off notification (because mail will be notify with slack)

When there are many connections from the following IP and its connected from related server of FAST RETAILING, dont setting deny, just you will inform to FR that the connection is load from target IP.

■ Target IP

0.0.0.0<br>
※If other target IP is increase, please correction and update the IP list.

## 2. Server List
----
Tokyo Region Monitoring Server: mnt01-a-tky-nagios-common (MobileApp)
----
| Down Work | Server Name | Global IP | Local IP | Server Info | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|
※2|mnt01-a-tky-nagios-common|-|10.184.232.10|mnt01-a-tky-nagios-common server info|PASSWD|Monitoring Server|
|※2|prd01-a-tky-log-mobileapp-uniqlo|-|10.184.16.12|prd01-a-tky-log-mobileapp-uniqlo server info|PASSWD|| |
|※2|prd02-a-tky-log-mobileapp-uniqlo|-|10.184.16.13|prd02-a-tky-log-mobileapp-uniqlo server info|PASSWD||
|※2|prd03-a-tky-push-mobileapp-uniqlo(Temporarily delete monitoring)|-|10.184.0.10|prd03-a-tky-push-mobileapp-uniqlo server info|PASSWD||
|※2|prd04-c-tky-push-mobileapp-uniqlo(Temporarily delete monitoring)|-|10.184.4.10|prd04-c-tky-push-mobileapp-uniqlo server info|PASSWD||
|※2|prd01-a-tky-manage-mobileapp-uniqlo|-|10.184.16.14|prd01-a-tky-manage-mobileapp-uniqlo server info|PASSWD||
|※2|prd01-a-tky-web-mobileapp-uniqlo|-|10.184.16.10|prd01-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|prd02-c-tky-web-mobileapp-uniqlo|-|10.184.20.10|prd02-c-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|prd03-a-tky-web-mobileapp-uniqlo|-|10.184.16.23|prd03-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|prd04-c-tky-web-mobileapp-uniqlo|-|10.184.20.23|prd04-c-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|prd05-a-tky-web-mobileapp-uniqlo|-|10.184.16.24|prd05-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|prd06-c-tky-web-mobileapp-uniqlo|-|10.184.20.24|prd06-c-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_mnt01-a-tky-ap-mobileappfeedback-uniqlo|-|10.184.192.14|ap-northeast-1_MobileApp_EC2_mnt01-a-tky-ap-mobileappfeedback-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_mnt01-a-tky-jenkins-mobileapp|-|10.184.248.12|ap-northeast-1_MobileApp_EC2_mnt01-a-tky-jenkins-mobileapp server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_prd01-a-tky-api-mobileapp-uniqlo|-|10.184.16.33|ap-northeast-1_MobileApp_EC2_prd01-a-tky-api-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_prd02-c-tky-api-mobileapp-uniqlo|-|10.184.20.33|ap-northeast-1_MobileApp_EC2_prd02-c-tky-api-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-log-mobileapp-uniqlo|-|10.184.80.18|ap-northeast-1_MobileApp_EC2_stg01-a-tky-log-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-manage-mobileapp-uniqlo|-|10.184.80.20|ap-northeast-1_MobileApp_EC2_stg01-a-tky-manage-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-batch-mobileapp-uniqlo|-|10.184.82.63|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-batch-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-log-mobileapp-uniqlo|-|10.184.82.173|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-log-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-manage-mobileapp-uniqlo|-|10.184.80.207|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-manage-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-mymail-mobileapp-uniqlo|-|10.184.66.32|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-mymail-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-mymanage-mobileapp-uniqlo|-|10.184.83.234|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-mymanage-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-web-mobileapp-uniqlo|-|10.184.83.251|ap-northeast-1_MobileApp_EC2_stg01-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-tky-web-mobileapp-uniqlo|-|10.184.80.15|ap-northeast-1_MobileApp_EC2_stg01-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-a-tky-log-mobileapp-uniqlo|-|10.184.80.19|ap-northeast-1_MobileApp_EC2_stg02-a-tky-log-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-a-tky-manage-mobileapp-uniqlo|-|10.184.80.27|ap-northeast-1_MobileApp_EC2_stg02-a-tky-manage-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-a-tky-mymail-mobileapp-uniqlo|-|10.184.64.21|ap-northeast-1_MobileApp_EC2_stg02-a-tky-mymail-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-a-tky-mymanage-mobileapp-uniqlo|-|10.184.80.28|ap-northeast-1_MobileApp_EC2_stg02-a-tky-mymanage-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-a-tky-web-mobileapp-uniqlo|-|10.184.80.16|ap-northeast-1_MobileApp_EC2_stg02-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg02-c-tky-stress-web-mobileapp-uniqlo|-|10.184.85.106|ap-northeast-1_MobileApp_EC2_stg02-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg03-a-tky-log-mobileapp-uniqlo|-|10.184.80.25|ap-northeast-1_MobileApp_EC2_stg03-a-tky-log-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg03-a-tky-push-mobileapp-uniqlo|-|10.184.64.10|ap-northeast-1_MobileApp_EC2_stg03-a-tky-push-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg03-a-tky-stress-push-mobileapp-uniqlo|-|10.184.65.125|ap-northeast-1_MobileApp_EC2_stg03-a-tky-stress-push-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg03-a-tky-stress-web-mobileapp-uniqlo|-|10.184.83.178|ap-northeast-1_MobileApp_EC2_stg03-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg03-a-tky-web-mobileapp-uniqlo|-|10.184.80.22|ap-northeast-1_MobileApp_EC2_stg03-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg04-a-tky-log-mobileapp-uniqlo|-|10.184.80.26|ap-northeast-1_MobileApp_EC2_stg04-a-tky-log-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg04-a-tky-push-mobileapp-uniqlo|-|10.184.64.11|ap-northeast-1_MobileApp_EC2_stg04-a-tky-push-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg04-a-tky-web-mobileapp-uniqlo|-|10.184.80.23|ap-northeast-1_MobileApp_EC2_stg04-a-tky-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg04-c-tky-stress-push-mobileapp-uniqlo|-|10.184.68.202|ap-northeast-1_MobileApp_EC2_stg04-c-tky-stress-push-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg04-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.133|ap-northeast-1_MobileApp_EC2_stg04-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg05-a-tky-push-mobileapp-uniqlo|-|10.184.64.24|ap-northeast-1_MobileApp_EC2_stg05-a-tky-push-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg05-a-tky-stress-web-mobileapp-uniqlo|-|10.184.80.123|ap-northeast-1_MobileApp_EC2_stg05-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg06-c-tky-stress-web-mobileapp-uniqlo|-|10.184.86.179|ap-northeast-1_MobileApp_EC2_stg06-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg07-a-tky-stress-web-mobileapp-uniqlo|-|10.184.81.199|ap-northeast-1_MobileApp_EC2_stg07-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg08-c-tky-stress-web-mobileapp-uniqlo|-|10.184.86.109|ap-northeast-1_MobileApp_EC2_stg08-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg09-a-tky-stress-web-mobileapp-uniqlo|-|10.184.81.198|ap-northeast-1_MobileApp_EC2_stg09-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg10-c-tky-stress-web-mobileapp-uniqlo|-|10.184.86.110|ap-northeast-1_MobileApp_EC2_stg10-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg11-a-tky-stress-web-mobileapp-uniqlo|-|10.184.82.23|ap-northeast-1_MobileApp_EC2_stg11-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg12-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.96|ap-northeast-1_MobileApp_EC2_stg12-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg13-a-tky-stress-web-mobileapp-uniqlo|-|10.184.82.22|ap-northeast-1_MobileApp_EC2_stg13-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg14-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.100|ap-northeast-1_MobileApp_EC2_stg14-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg15-a-tky-stress-web-mobileapp-uniqlo|-|10.184.82.20|ap-northeast-1_MobileApp_EC2_stg15-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg16-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.99|ap-northeast-1_MobileApp_EC2_stg16-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg17-a-tky-stress-web-mobileapp-uniqlo|-|10.184.82.19|ap-northeast-1_MobileApp_EC2_stg17-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg18-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.98|ap-northeast-1_MobileApp_EC2_stg18-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg19-a-tky-stress-web-mobileapp-uniqlo|-|10.184.82.18|ap-northeast-1_MobileApp_EC2_stg19-a-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg20-c-tky-stress-web-mobileapp-uniqlo|-|10.184.87.97|ap-northeast-1_MobileApp_EC2_stg20-c-tky-stress-web-mobileapp-uniqlo server info|PASSWD||
|※2|ap-northeast-1_MobileApp_EC2_stg01-a-jp-appdownload-mobileapp-uniqlo|-|10.184.64.18|[ap-northeast-1_MobileApp_EC2_stg01-a-jp-appdownload-mobileapp-uniqlo server info]|PASSWD||
|※2|prd07-a-tky-web-mobileapp-uniqlo|-|10.184.16.25|prd07-a-tky-web-mobileapp-uniqlo server info|PASSWD|Only scale-out operation|
|※2|prd08-c-tky-web-mobileapp-uniqlo|-|10.184.20.25|prd08-c-tky-web-mobileapp-uniqlo server info|PASSWD|Only scale-out operation|
|※2|prd09-a-tky-web-mobileapp-uniqlo|-|10.184.16.26|prd09-a-tky-web-mobileapp-uniqlo server info|PASSWD|Only scale-out operation|
|※2|prd10-c-tky-web-mobileapp-uniqlo|-|10.184.20.26|prd10-c-tky-web-mobileapp-uniqlo server info|PASSWD|Only scale-out operation|
|※2|RDS_prd01-mobileapp-datastore|-|-|-|-|RDS:no login allowed|
|※2|RDS_prd01-mobileapp-datastore|-|-|-|-|RDS:no login allowed|
|※2|RDS_prd01-mobileapp-datastore-read|-|-|-|-|RDS:no login allowed|
|※2|RDS_prd01-mobileapp-datastore-shard01|-|-|-|-|RDS:no login allowed|
|※2|RDS_prd01-mobileapp-datastore-shard02|-|-|-|-|RDS:no login allowed|
|※2|RDS_prd01-mobileapp-account|-|-|-|-|RDS:no login allowed|
|※2|ElastiCache_prd01-mobileapp|-|-|-|-|ElastiCache:no login allowed|~
|※2|ElastiCache_prd02-mobileapp|-|-|-|-|ElastiCache:no login allowed|

#### nrpe Command:

* nrpe Restart Command (※ command execute the following in below command from the monitoring server)
  /home/nnet/script/remote_nrpe_restart IP Address<br>
    「-i option OK? [n]: 」to display, Type a [y] and enter ※after execute this command、it will take some times.<br>
    「-i option OK? [n]: 」to display, if type a [n] then becomes cancel from this command.

* nrpe Start Command<br>
/home/nnet/nrpe/src/nrpe -d /home/nnet/nrpe/nrpe.cfg

Sample event of after execute this command:<br> #/home/nnet/script/remote_nrpe_restart

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
---
|URL Monitoring Contents|Object URL|Remarks|If not recovery after primary operation|
| :----------:|:------------:|:------------:|:------------:|
|URL_mobileapp.uniqlo.com_POST|http://mobileapp.uniqlo.com/jp/api/200/|Status Code「200 OK」|・contact by phone for short time detected alert<br>・if an alert is detected from other URL then contact to phone<br><br>・After primary operation but is not recovery and there is an impact on the service then contact by phone|

#### Tokyo Region<br>
Monitoring Server: mnt01-a-tky-nagios-common<br>
Monitoring Server: mnt01-a-tky-nagios-common (MobileApp_ELB)

|HOST Object|Contents|Procedure to primary Operation|Procedure to manual check|If not recovery after primary operation|
| :----------:|:------------:|:------------:|:------------:|:------------:|
|ELB_uniqlo_MobileApp_tky_web_URL|-|prd*-*-tky-web-mobileapp apache restart|Visual check of target URL|After primary operation but is not recovery and there is an impact on the service then contact by phone|
|ELB_uniqlo_MobileApp_tky_mymanage_URL|-|prd01-a-tky-mymanage-mobileapp apache restart|Visual check of target URL|After primary operation but is not recovery and there is an impact on the service then contact by phone|
|ELB_uniqlo_MobileApp_tky_manage_URL|-|prd01-a-tky-manage-mobileapp apache restart|Visual check of target URL|After primary operation but is not recovery and there is an impact on the service then contact by phone|
|ELB_uniqlo_MobileApp_tky_api_URL|-|prd01-a-tky-api-mobileapp<br>prd02-a-tky-api-mobileapp apache restart|Visual check of target URL|After primary operation but is not recovery and there is an impact on the service then contact by phone|
|MobileApp_ELB|ELB_Latency_prd01-web-mobileapp-uniqlo|report to email average value of additional info|May_Day|-|

|Monitoring Contents|Procedure to primary Operation/Command|Procedure to manual check|
| :----------:|:------------:|:------------:|
|DOWN<br>SSH|Server Restart|May_Day|
|DOWN※Multiple Server※|Follow the FR project manual when the multiple server DOWN|Ping Check from monitoring server and status check on the AWS console management|
|PROCS_SSH|/etc/init.d/sshd restart<br>if recovery, after execute above command then report to related in internal team,<br>if not recovery then report to client by email|May_Day|
|VPN Failure|Follow to VPN manual when a VPN failure occurs|-|
|CPU|If there is no impact on other monitoring contents then report to email the cause of load<br>If there is an impact on other monitoring contents then take action<br>※In the case of RDA, report to email of current value listed in additional info|/home/nnet/script/check_cpu 80 90|
|LOAD|If there is no impact on other monitoring contents then report to email the cause of load<br>If there is an impact on other monitoring contents then take action|/home/nnet/libexec/check_load -w 5,10,15 -c 10,15,20|
|NTP|(1) ntpd restart<br> /etc/rc.d/init.d/ntpd (stop/start/restart)<br>↓<br>(2) If not recovery, Changing the destination server of ntp.conf to ntp server of Amazon and restart ntpd<br>After restart ntpd:<br>⇒ If recovery, no need any other action<br>⇒ If not recovery, then contact by email|/home/nnet/script /check_ntp|
|SMTP|/etc/init.d/sendmail (stop/start/restart)|/home/nnet/libexec/check_smtp -H localhost|
|SWAP|After execute restart/stop of cause process and contact to email|/home/nnet/libexec/check_swap -w 70% -c 50%|
|DISK_/|■ Case of bellow server<br>Follow the refer mobileapp_log delete manual<br>◇Target Server<br>・prd01-a-tky-web-mobileapp-uniqlo/10.184.16.10<br>・prd02-c-tky-web-mobileapp-uniqlo/10.184.20.10<br>・prd03-a-tky-web-mobileapp-uniqlo/10.184.16.23<br>・prd04-c-tky-web-mobileapp-uniqlo/10.184.20.23<br>・prd05-a-tky-web-mobileapp-uniqlo/10.184.16.24<br>・prd06-c-tky-web-mobileapp-uniqlo/10.184.20.24<br>when delete is complete and get to backup on the S3 then inform to client by email of the regarding backup and delete operation.<br>----<br>■ for above the other than server<br>report to email usage status|/home/nnet/libexec/check_disk -w 20% -c 10% -p /|
|DISK_/mnt|・If the case of unmount, to execute mount the following command<br>　mount -a<br>・prd01-a-tky-log-mobileapp-uniqloのDISK_/mnt in case of alert<br>①lsof -c rsyslog, check the rsyslog, if holds deleted log in rsyslog then go to step ③ if are not holds then go to step ②<br>②rsyslog restart and check DISK space<br>/etc/rc.d/init.d/rsyslog (stop/start) ※not execute restart command ！！！<br>after restart and check the movement status using below command<br>netstat -lntup | grep rsyslogd | grep LISTEN<br>check the 514 port no is display.<br>If any other problem is detected, escalation with related team.|/home/nnet/libexec/check_disk -w 20% -c 10% -p /mnt|
|MAILQ|escalation with related team have any detect alert|/home/nnet/libexec/check_mailq -w 50 -c 100|
|TCP-memcached|If restart on the Elastic Cache, confirm and check with the related in charge dev team|May_day|
|MYSQL|Host: Case of RDS: Contact to phone<br>Contact: Normal contact and related in charge team|MayDay|
|*LOG|※Point notes: If detected object logs are related to "ldap" logs then no need to contact !!。<br><br>1. contact to email of the log contents by reference to Additional Info<br>2. move to lock file<br><br>※How to find the lock file<br>for mystoreadm-LOG<br>① Find the script of the target contents from the check command of nrpe<br>less /home/nnet/nrpe/nrpe.cfg<br>command[check_log-mystoreadm]=/home/nnet/script/check_log-mystoreadm.sh<br><br>② Check the script<br>less/home/nnet/script/check_log-mystoreadm.sh<br>(Excerpt)<br>LOCK='/home/nnet/script/LOGS/mystoreadms/mystoreadm.lock'<br><br>③ Check by ll command<br>ll /home/nnet/script/LOGS/mystoreadms/mystoreadm.lock<br>-rw-r--r-- 1 root root 0 Dec 12 06:52 /home/nnet/script/LOGS/mystoreadms/mystoreadm.lock<br>④ Move if the lock file is created<br>mv /home/nnet/script/LOGS/mystoreadms/mystoreadm.lock{,.old}<br><br>【In the case of spr-LOG contents】<br>■ Check the target log following below command<br># cat /var/log/spr/spr.log / grep "FATAL"<br># cat /var/log/spr/spr.log / grep -i "ERROR"<br>※spr-LOG contents does not generate lock file, and  confirm to make recovery email after recovery.<br>※1Alerts detected at 12 o'clock are possibility rotate.|May_day|
|uniqlo_api_error-LOG|/home/nnet/script/LOGS/api_error/NG-logs.diff_error<br>/home/nnet/script/LOGS/api_error/NG-logs.diff_warn<br>Check the above command and contact to email<br>■ After contacting email<br>move to lock file <br>/home/nnet/script/LOGS/api_error/api_error.lock|May_day|
|uniqlo_api_error-LOG2|※This alert can be detected when the specific keywords are output in the log of 100 or 300 in one hour.<br>■ Operation Procedure<br>1.All of the following in below ①～③ are carried out by the alert detection server<br>① cat /home/nnet/script/LOGS/api_error/NG-logs2_error / wc -l<br>② cat /home/nnet/script/LOGS/api_error/NG-logs2_warn / wc -l<br>③ cat /home/nnet/script/LOGS/api_error/NG-logs2_error2 / wc -l<br><br>2. The following「1.」of in below operation<br>① If the execution result of exceeds 100 in total within one hour<br>「ERROR_HANDLING」と「ERROR_API_NOT_FOUND」<br>Then report to email the target log<br>② If the execution result of exceeds 100 in total within one hour「ERROR_PARAMETER_UNDEFIND」and「ERROR_AUTHKEY_INVALID」and「ERROR_SESSION_INVALID」<br>Then report to email the target log<br>③ If the execution result of exceeds 300 in total within one hour<br>「ERROR_NO_USER_DATA」<br>Then report to email the target log<br><br>※Notes: ①～③ In case of multiple execution results, all of them are becomes target contact.<br>3. After contacting email:<br>/home/nnet/script/LOGS/api_error/api_error2.lock to move<br>mv /home/nnet/script/LOGS/api_error/api_error2.lock{,.old}|May_day|
|mail-LOG|/var/log/apps/mystore/mail.YYYYMMDD.log check from this log and report to email error contents<br>after contacting email, move the lock file below command<br>/home/nnet/script/LOGS/mail/mail.lock<br>mv /home/nnet/script/LOGS/mail/mail.lock{,.old}|May_day|
|URL*| *-tky-web-mobileapp-uniqlo check of HTTP etc. and restart to apache on the target server<br>■ Restart command<br>/etc/init.d/httpd (stop/start/restart)<br>※After primary operation , and if not recovery and there is an impact on the service then follow the reference related manual||
|HTTP|/etc/init.d/httpd (stop/start/restart)|May_day|
|TCP-10080<br>PROCS_perl|■ Stop command<br>kill [PID]<br>■ Start command<br>/service/app-push-engine-global/run|・TCP-10080<br>May_day<br><br>・PROCS_perl<br>/home/nnet/libexec/check_procs -c 1: -a<br> "/usr/bin/perl /var/lib/sprush/app-push-engine-global/current/push/push_notification_server.pl"|
|push-segment-LOG|after email, move to lock file|May_day|
|td-agent-SEND|/etc/rc.d/init.d/td-agent (stop/start/restart)<br>If the following is output, delete the lock file and observation monitoring<br>[warn]: retry succeeded.|May_day|
|PROCS_td-agent|/etc/rc.d/init.d/td-agent (stop/start/restart)|May_day|
|PROCS_CRON|/etc/rc.d/init.d/crond (stop/start/restart)<br>If is recovery, report to internal email related in team <br>If not recovery, contact to email with client.|May_day|
|PROCS_RSYSLOG|/etc/rc.d/init.d/rsyslog (stop/start/restart)<br>If is recovery, report to internal email related in team <br>If not recovery, contact to email with client.|May_day|
|FreeStorageSpace|contact to email of current value listed in additional Info<br>Sample:<br>Additional Info:<br>CRITICAL AWS/RDS FreeStorageSpace ～～ Average: **********<br>↓<br>it becomes sample of current values.<br>************（byte）|May_Day|
|Latency|report to email current values listed at Additional Info|May_Day|
|uniqlo_api_apache_syslog-NOT-WORK|① Check the below all processes are activated<br>ps ax grep apache_syslog<br><br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.push.error_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.img.error_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.api.error_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.web.error_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.push.access_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.push.sprush_access_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.img.access_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.api.access_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.web.access_log local0<br>/usr/bin/perl /usr/local/bin/apache_syslog app-web.web.track_access_log local0<br><br>② If not running then execute command apache graceful<br>sudo /etc/init.d/httpd graceful<br>③ Check above all the process are activated, and report to email of the result<br>ps ax grep apache_syslog|May_Day|

## 4. How to Restart the Server
-----
##### ※ Follow the instruction of the AWS Restart Manual

Restart event is follow the "reboot" execute<br>
※Dont follow the stop/start  execute for restart event

If a case require to stop/start execute then escalate to related in-charge team and report current situation<br>

#### * Check the following requires when executing the ELB detaching operation:<br>
 
1. Check and confirm the target server to remove from ELB on the AWS management console
2. Check access log of the server (/var/log/httpd/access_log),<br>
and Login each server to remove from ELB and confirm the access yes/no from the user.
3. If access is possible to execute of ELB detaching by the above procedure(2) then,<br>
Rollback ELB ⇒ Detaching operation is execute again

## 5. Emergency Contact
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and English template.
<br>
##### [By using Japanese and English mail Template]

■Contact email address:<br>

To:    <br>
Cc:    <br>

■Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1||	 
|2|||

## 7. Submit to troubleshooting Report:
------

Not Necessary.

----------------------------------



