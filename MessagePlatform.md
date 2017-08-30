
## MessagePlatform Operation Manual

## Contents

1. Specific Remarks<br> 
2. Server List<br>
3. Operation Procedure<br>
4. How to Restart the Server<br>
5. JIRA Info<br>
6. Emergency Contact<br>
7. Submit to Troubleshooting Report

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
Monitoring Server: mnt01-a-tky-nagios-common　※To connect via the platform of Bastion Server
----
| Down Work | Server Name | Global IP | Local IP | Server Info | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|
|※2|mnt01-a-tky-gateway-common|54.250.223.60|-|mnt01-a-tky-gateway-common server info|PASSWD|Bastion Platform Server|
※1|mnt01-a-tky-nagios-common|-|10.184.232.10|mnt01-a-tky-nagios-common server info|PASSWD|Monitoring Server|
|※2|prd01-a-tky-bzapi-message|-|10.184.19.115|prd01-a-tky-bzapi-message server info|PASSWD|API server(Biz) ※autoscale base AMI instance|
|※2|prd01-a-tky-admin-message|-|10.184.18.70|prd01-a-tky-admin-message server info|PASSWD|CMS server|
|※2|prd01-a-tky-delivery-controller-message|-|10.184.19.26|prd01-a-tky-delivery-controller-message server info|PASSWD|Delivery controller|
|※2|prd01-a-tky-extraction-woker-message|-|10.184.17.81|prd01-a-tky-extraction-woker-message server info|PASSWD|Extract worker ※autoscale base AMI instance|
|※2|prd01-a-tky-extraction-woker-message-04|-|10.184.16.42|prd01-a-tky-extraction-woker-message-04 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-extraction-woker-message-05|-|10.184.16.55|prd01-a-tky-extraction-woker-message-05 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-extraction-woker-message-06|-|10.184.16.52|prd01-a-tky-extraction-woker-message-06 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-extraction-woker-message-07|-|10.184.16.51|prd01-a-tky-extraction-woker-message-07 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-extraction-woker-message-08|-|10.184.16.60|prd01-a-tky-extraction-woker-message-08 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-extraction-woker-message-09|-|10.184.16.57|prd01-a-tky-extraction-woker-message-09 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-05|-|10.184.20.157|prd01-c-tky-extraction-woker-message-05 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-06|-|10.184.20.159|prd01-c-tky-extraction-woker-message-06 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-07|-|10.184.20.163|prd01-c-tky-extraction-woker-message-07 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-08|-|10.184.20.161|prd01-c-tky-extraction-woker-message-08 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-09|-|10.184.20.156|prd01-c-tky-extraction-woker-message-09 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-extraction-woker-message-10|-|10.184.20.158|prd01-c-tky-extraction-woker-message-10 server info|PASSWD|Extract worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-delivery-woker-message|-|10.184.0.250|prd01-a-tky-delivery-woker-message server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-01|-|10.184.1.121|prd01-a-tky-delivery-woker-message-01 server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-02|-|10.184.1.123|prd01-a-tky-delivery-woker-message-02 server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-03|-|10.184.1.122|prd01-a-tky-delivery-woker-message-03 server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-04|-|10.184.1.125|prd01-a-tky-delivery-woker-message-04 server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-05|-|10.184.1.124|prd01-a-tky-delivery-woker-message-05 server info|PASSWD|Delivery worker|
|※2|prd01-a-tky-delivery-woker-message-06|-|10.184.1.126|prd01-a-tky-delivery-woker-message-06 server info|PASSWD|Delivery worker ※Monitoring delete temporarily|
|※2|prd01-c-tky-delivery-woker-message-07|-|10.184.4.57|prd01-c-tky-delivery-woker-message-07 server info|PASSWD|Delivery worker ※Monitoring delete temporarily|
|※2|prd01-a-tky-immediate-delivery-woker-message|-|10.184.2.243|prd01-a-tky-immediate-delivery-woker-message server info|PASSWD|Immediate delivery worker|
|※2|prd01-a-tky-statusupdate-woker-message|-|10.184.17.37|prd01-a-tky-statusupdate-woker-message server info|PASSWD|error processing worker ※autoscale base AMI instance|
|※2|prd01-c-tky-jenkins-message|-|10.184.20.107|prd01-c-tky-jenkins-message server info|PASSWD|-|
|※2|mng01-c-tky-jenkins-message|-|10.184.236.201|mng01-c-tky-jenkins-message server info|PASSWD|-|
|※2|stg01-c-tky-jenkins-message|-|10.184.87.78|stg01-c-tky-jenkins-message server info|PASSWD|-|
|※2|prd01-c-tky-immediate-delivery-woker-message|-|10.184.6.162|prd01-c-tky-immediate-delivery-woker-message server info|PASSWD|Immediate delivery worker|
|Monitoring obsevation|API-message_[IP]|-|-|-|PASSWD|API server(Consumer) AutoScaling server group|
|Monitoring obsevation|receipt-woker-MessagePF_[IP]|-|-|-|PASSWD|List entry reception processing worker AutoScaling server group|
|Monitoring obsevation|bzapi-MessagePF_[IP]|-|-|-|PASSWD|API server(Biz) AutoScaling server group|
|Monitoring obsevation|extraction-MessagePF_[IP]|-|-|-|PASSWD|Extract worker AutoScaling server group|
|Monitoring obsevation|delivery-MessagePF_[IP]|-|-|-|PASSWD|Timer delivery worker AutoScaling server group|
|Monitoring obsevation|immediate-delivery-MessagePF_[IP]|-|-|-|PASSWD|Immediate delivery worker AutoScaling server group|
|Monitoring obsevation|statusupdate-MessagePF_[IP]|-|-|-|PASSWD|Error status update worker AutoScaling server group|
|※2|RDS_prd01-tky-messageplatform|-|-|-|-|RDS:no login allow|
|※2|RDS_messagedevice|-|-|-|-|RDS:no login allow|
|※2|RDS_prd01-tky-device-message-fr|-|-|-|-|RDS:no login allow|
|※2|RDS_prd02-tky-device-message-fr|-|-|-|-|RDS:no login allow|
|※2|RDS_prd03-tky-device-message-fr|-|-|-|-|RDS:no login allow|
|※2|RDS_prd04-tky-device-message-fr|-|-|-|-|RDS:no login allow|

nrpe Command:

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

■ ELB Monitoring<br>
Monitoring Server (mnt01-a-tky-nagios-common)

|Target ELB Monitoring|Monitoring Contents|Interval| Remarks |Primary operation |Procedure to Manual Check|JIRA| Remarks|
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|:----------:|
|ELB_prd01-tky-admin-message|HealthyHostCount|1|When the number of EC2 under the ELB falls below the threshold then detect problems|email contact with client|May_Day|-|ELB(CMS)|
|ELB_prd01-tky-api-message|ELB_Latency|1s|[HTTP listener] the request send to the load balancer and until the response header is received, its measure elapsed time(s)|Average value of additional info report to email and phone|May_Day|-|ELB(API(Consumer))|
|ELB_prd01-tky-api-message|HealthyHostCount|10|When the number of EC2 under the ELB falls below the threshold then detect problems|Average value of additional info report to email and phone|May_Day|-|ELB(API(Consumer))|
|ELB_prd01-tky-bzapi-message|ELB_Latency|5s|[HTTP listener] the request send to the load balancer and until the response header is received, its measure elapsed time(s)|Average value of additional info report to email and phone|May_Day|-|ELB(API(Biz))|
|ELB_prd01-tky-bzapi-message|HealthyHostCount|2|When the number of EC2 under the ELB falls below the threshold then detect problems|email and Phone contact with client|May_Day|-|ELB(API(Biz))|

■ RDS Monitoring<br>
Monitoring Server (mnt01-a-tky-nagios-common)

|Target ELB Monitoring|Monitoring Contents|Interval| Remarks |Primary operation |Procedure to Manual Check|JIRA| Remarks|
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|:----------:|
|RDS_prd01-tky-device-message,<br>RDS_prd02-tky-device-message,<br>RDS_prd03-tky-device-message,<br>RDS_prd04-tky-device-message|CPU_Utilization|80|If the threshold is exceeded, then detect an alert|email contact with client|May_Day|-|RDS|


## 3. Operation Procedure
---
|Monitoring Contents|Procedure to Primary Operation/Command|Procedure to manually check|JIRA|
|:-----:|:-----:|:------:|:------:|
|SSH/PROCS_SSH|**In the case of Delivery Controller:**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>Instance Restart|May_Day|-|
|CPU|**In case of RDS, API server server(Consumer),API server(Biz):**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>When there is no impact on other monitoring contents then email to report cause of load,<br>When there is an impact on other monitoring contents, then take action<br>In the case of RDS, email to report the current value described in additional info|May_Day|-|
|LOAD|**In case of API server server(Consumer),API server(Biz):**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>When there is no impact on other monitoring contents then email to report cause of load,<br>When there is an impact on other monitoring contents, then take action|/home/nnet/libexec/check_load -w 5,10,15 -c 10,15,20|-|
|SWAP|When there is no impact on other monitoring contents then email to report cause of load,<br>When there is an impact on other monitoring contents, then take action|/home/nnet/libexec/check_swap -w 70% -c 70%|-|
|DISK_/*|**In the case of API server server(Consumer),API server(Biz), CMS server,Delivery controller, delivery worker, Immediate delivery worker,error status update worker, list entry processing worker, Extract worker:**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>email to report usage status|/home/nnet/libexec/check_disk -w 20% -c 10% -p /*|-|
|NTP|**In the case of API server server(Consumer),API server(Biz), CMS server,Delivery controller, delivery worker, Immediate delivery worker,error status update worker, list entry processing worker, Extract worker:**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>/etc/rc.d/init.d/ntpd (stop/start/restart)<br>If not recovery after ntpd restart then take action below<br><br>**above the others server** Normal operation and email to report|/home/nnet/script/check_ntp|-|
|HTTP|**In the case of API server server(Consumer),API server(Biz), CMS server:**<br>Normal Operation and phone contact<br>**Normal Operation:**<br>contact email only (if detect an alert then do escalation and cause analysis|MayDay|-|
|URL_prd01-a-tky-jenkins-storecatalog|contact email|MayDay|-|
|PROCS_SUPERVISOR PROCS_SUPERVISOR_CHILD_FATAL|**In the case of Extrat worker, Delivery worker, Immediate worker, List entry processing worker:**<br>Normal Operation and phone contact(case of phone contact, check below ※1 or <br>※ 1. If re  cover by primary operation, contact to email only, if not recovery contact to phone + email<br> ※2. In the case of intermittently detection recovery, contact to phone communication, when appropriate operation is applied and confirmed calm then contact to email<br>Normal Operation:**<br>contact email only (if detect an alert then do escalation and cause analysis･<br>**Normal Operation:** ・root user<br>#supervisorctl status　※status check<br># supervisorctl restart all|■PROCS_SUPERVISOR<br>/home/nnet/libexec/check_procs -c 1: -a "<br>/usr/bin/python2.7 /usr/local/bin/supervisord -c /etc/supervisord.conf" -p 1<br>■PROCS_SUPERVISOR_CHILD_FATAL<br>/home/nnet/script/check_supervisor_child_fatal.sh|-|
|apache-LOG|※In the case of this log message is exist 「File does not exist」, not need to action<br><br>/var/log/httpd/ log monitoring of log in bellow<br>■ Case detection<br>if have 500 response more than 10 times per hour then alert<br>※must be check raw log, above「■ case detection」checked and confirm<br>■ Operation Procedure<br>・Case of API server(Biz)<br>Normal operation and phone contact<br>・Normail Operation<br>report to email of latest log of target detection<br>/home/nnet/script/messagepf.lock|May_Day|-|
|app-LOG-CRITICAL|■ CMS Server<br>/var/log/app/message_admin_app.log monitoring<br>when [CRITICAL] alert appears more than one in the log<br>then report to email and phone contact with latest log of the target detection<br>※The following lock file is generated that why do rename after operation<br>mv /home/nnet/script/log/message_admin_app.log.lock{,.old}<br><br>----------<br>■ Extraction worker server<br>/var/log/app/message_pack_worker_app.log monitoring<br>when [CRITICAL] alert appears more than three of 5 intervals time in the log<br>then report to email and phone contact with latest log of the target detection<br>※The following lock file is generated that why do rename after operation<br>mv /home/nnet/script/log/appCRITICAL.lock{,.old}<br><br>----------<br>■ Delivery worker server<br>/var/log/app/message_timer_delivery_worker_app.log monitoring<br>when [CRITICAL] alert appears more than three of 5 intervals time in the log<br>then report to email and phone contact with latest log of the target detection<br>※The following lock file is generated that why do rename after operation<br>mv /home/nnet/script/log/appCRITICAL.lock{,.old}<br><br>----------<br>■ Immediate delivery worker<br>/var/log/app/message_immediate_delivery_worker_app.log monitoring<br>when [CRITICAL] alert appears more than three of 5 intervals time in the log<br>then report to email and phone contact with latest log of the target detection<br>※The following lock file is generated that why do rename after operation<br>mv /home/nnet/script/log/appCRITICAL.lock{,.old}<br><br>----------<br>|May_Day|-|
|timer-extraction-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-extraction-LOG-CRITICAL @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_pack_controller_app.log monitoring<br>when [CRITICAL] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-extraction-LOG-WARNING|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-extraction-LOG-WARNING @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_pack_controller_app.log monitoring<br>when [WARNING] alert appears more than two per hour in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-delivery-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-delivery-LOG-CRITICAL @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_timer_delivery_controller_app.log monitoring<br>when [CRITICAL] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-delivery-LOG-WARNING|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-delivery-LOG-WARNING @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_timer_delivery_controller_app.log monitoring<br>when [CRITICAL] alert appears more than two in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|status-update-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:status-update-LOG-CRITICAL @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_delivery_status_controller_app.log monitoring<br>when [CRITICAL] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|status-update-DELAYED_EXTRACTION|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:status-update-DELAYED_EXTRACTION @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_delivery_status_controller_app.log monitoring<br>when [EXTRACTION_PROCESS_IS_DELAYED ] alert appears more than two in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|status-update-DELAYED_DELIVERY|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:status-update-DELAYED_DELIVERY @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_delivery_status_controller_app.log monitoring<br>when [DELIVERY_PROCESS_IS_DELAYED] alert appears more than two in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-delivery-NO_DELIVERY_DATA|■ In case of the delivery controller<br>required to phone contact<br><br>If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-delivery-NO_DELIVERY_DATA @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_timer_delivery_controller_app.log monitoring<br>when [TIMER_DELIVERY_NO_DELIVERY_DATA] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-delivery-LOW_EXTRACTION_RATE|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-delivery-LOW_EXTRACTION_RATE @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_delivery_status_controller_app.log monitoring<br>when [EXTRACTION_RATE_IS_TOO_LOW] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|timer-delivery-LOW_DELIVERY_RATE|If automatic mail is transmitted normally, no email contact is required<br>◇Target mail title:timer-delivery-LOW_DELIVERY_RATE @ prd01-a-tky-delivery-controller-message<br><br>/var/log/app/message_delivery_status_controller_app.log monitoring<br>when [DELIVERY_RATE_IS_TOO_LOW] alert appears more than one in the log<br>then report to email with latest log of the target detection<br>※The lock file is not generated|May_Day|-|
|app-LOG-WARNING|■ Operation Manual<br>☆Case Detection<br>When [WARNING] is more than two in last hour in the log of target monitored, is required to contact.<br><br>☆Operation Procedure<br>/home/nnet/script/log/appWARNING/appWARNING.diffall, it checks, and there are more than two [WARNING] is detection alert then report to log by email<br> If the beginning of the sentence are sign "<" is attached then within one hour log is contacted object.<br>
※ But the sign ">" is attached of the beginning sentence, so this is impact of rotate, and its ignore and OK !!<br>※The lock file is not generated<br><br>☆Recovery Operation<br>It will not recover for one hour, so if you want to recover manually then delete unnecessary logs from this file<br>/home/nnet/script/log/appWARNING/appWARNING.diff1 - 12<br>■ Extraction worker server<br>----------<br>/var/log/app/message_pack_worker_app.log monitoring<br>--------<br>■ Error status Update worker<br>/var/log/app/message_error_feedback_worker_app.log monitoring<br>-------<br>■ Delivery worker<br>/var/log/app/message_timer_delivery_worker_app.log monitoring<br>-------<br>■ Immediate delivery worker<br>/var/log/app/message_immediate_delivery_worker_app.log monitoring<br>-------<br>■ List entry processing worker<br>/var/log/app/message_delivery_list_receipt_worker_app.log monitoring|/home/nnet/script/check_appWARNING.sh 【log of object monitoring】<br>　■ Extraction worker server<br>　/home/nnet/script/check_appWARNING.sh<br>message_pack_worker_app.log<br>　■ Error status update worker<br>　/home/nnet/script/check_appWARNING.sh<br>message_error_feedback_worker_app.log<br>　■ Delivery worker<br>　/home/nnet/script/check_appWARNING.sh<br>message_timer_delivery_worker_app.log<br>　■ Immediate delivery worker<br>　/home/nnet/script/check_appWARNING.sh<br>message_immediate_delivery_worker_app.log<br>　■ List entry processing worker<br>　/home/nnet/script/check_appWARNING.sh<br>message_delivery_list_receipt_worker_app.log<br><br>※ Checking cron from log of case detection<br>※AutoScaling server group, the following script needs to be manually modified until AMI is updated※<br><br>*/5 * * * * /bin/bash /home/nnet/script/cron_appWARNING.sh 【Log of object monitoring】|-|
|extraction-jenkins-NOT-WORK<br>timer-delivery-jenkins-NOT-WORK<br>status-update-jenkins-NOT-WORK<br>messagebox_old_purge-NOT-WORK<br>log_collect-jenkins-NOT-WORK<br>all_member_ids-jenkins-NOT-WORK|・In case jenkins server<br>Normal Operation and phone contact<br>・Normal Operation<br>NOT-WORK alert operation|May_Day|-|
|PROCS_CROND|/etc/rc.d/init.d/crond (stop/start/restart)<br>If the case of recovery then report to internal related team<br>But if not recovery then contact to client by email|/home/nnet/libexec/check_procs -c 1: -a "crond" -p 1|-|
|PROCS_SYSLOGD|/etc/rc.d/init.d/rsyslog (stop/start/restart)<br>If the case of recovery then report to internal related team<br>But if not recovery then contact to client by email|/home/nnet/libexec/check_procs -c 1: -a "/sbin/rsyslogd"|-|
|PROCS_munin<br>PROCS_munin-node|/etc/rc.d/init.d/munin-node (stop/start/restart)<br>If the case of recovery then report to internal related team<br>But if not recovery then contact to client by email|/home/nnet/libexec/check_procs -c 1: -a "/usr/sbin/munin-node"|-|
|PROCS_LOGSTASH|/etc/rc.d/init.d/logstash (stop/start/restart)
<br>If the case of recovery then report to internal related team<br>But if not recovery then contact to client by email|/home/nnet/libexec/check_procs -c 1: -a "logstash"/usr/sbin/munin-node"|-|
|FreeStorageSpace|contact to email the current value listed in Additional Info|May_Day|-|
|Latency|contact to email the current value listed in Additional Info|May_Day|-|
|[NNET-ONLY]-app-LOG-WARNING|Not required action<br>report to internal related team|May_Day|-|
|old_message_purge-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>/var/log/app/message_old_message_purge_app.log monitor<br>when [CRITICAL] alert appears more than one in the log<br>then report to latest log by email<br>※The lock file is not generated|May_Day|-|
|old_message_purge-LOG-WARNING|/var/log/app/message_old_message_purge_app.log monitor<br>when [WARNING] alert appears more than two per hour in the log<br>then report to latest log by email<br>※The lock file is not generated|May_Day|-|
|log_collect-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>/var/log/app/message_member_message_log_collect_app.log monitor<br>when [CRITICAL] alert appears more than one in the log<br>then report latest log by email<br>※The lock file is not generated|May_Day|-|
|log_collect-LOG-WARNING|/var/log/app/message_member_message_log_collect_app.log monitor<br>when [WARNING] alert appears more than two per hour in the log<br>then report to latest log by email<br>※The lock file is not generated|May_Day|-|
|all_member_ids-LOG-CRITICAL|■ In case of the delivery controller<br>required to phone contact<br><br>/var/log/app/message_pack_controller_all_member_ids_app.log monitor<br>when [CRITICAL] alert appears more than one in the log<br>then report latest log by email<br>※The lock file is not generated|May_Day|-|
|all_member_ids-LOG-WARNING|/var/log/app/message_pack_controller_all_member_ids_app.log monitor<br>when [WARNING] alert appears more than two per hour in the log<br>then report to latest log by email<br>※The lock file is not generated|May_Day|-|

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

## 5. JIRA Info
-----

## 6. Emergency Contact
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and english template.
<br>
##### [By using Japanese and english mail Template]

■Contact email address:<br><br>

For Resource Monitoring:<br>

To:    <br>
Cc:    <br>

For LOG Monitoring:<br>

To:    <br>
Cc:    <br>

* Target log Items:<br><br>
apache-LOG<br>app-LOG-CRITICAL<br>app-LOG-WARNING<br>old_message_purge-LOG-CRITICAL<br>log_collect-LOG-CRITICAL<br>log_collect-LOG-WARNING<br>all_member_ids-LOG-CRITICAL<br>all_member_ids-LOG-WARNING<br><br>timer-extraction-LOG-CRITICAL<br>timer-extraction-LOG-WARNING<br>timer-delivery-LOG-CRITICAL<br>timer-delivery-LOG-WARNING<br>status-update-LOG-CRITICAL<br>status-update-DELAYED_EXTRACTION<br>status-update-DELAYED_DELIVERY<br>timer-delivery-NO_DELIVERY_DATA<br>timer-delivery-LOW_EXTRACTION_RATE<br>timer-delivery-LOW_DELIVERY_RATE<br>

■Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1||	 
|2|||

## 7. Submit to troubleshooting Report:
------

Not Necessary.

----------------------------------



