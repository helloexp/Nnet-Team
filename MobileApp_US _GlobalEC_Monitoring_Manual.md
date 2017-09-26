
## MobileApp US GLOBAL EC Monitoring Manual

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

The following settings are necessary to browser of each Server and Nagios at this project.<br>

 * Require to VPN connection for FR project.

You are notified to customers via slack when alert occurs in all new infra projects, but if you receive a large amount of alerts then there may be need to inquiries to customers.

## 2. Server List
----
Monitoring Server for MobileApp
----
| Type | Server Name | Local IP | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|
|EC2|Monitoring Server|-|-|-|	
|EC2|prd01-a-vir-batch-mobileapp-uq|10.177.17.220|PASSWD|-|	
|EC2|prd01-a-vir-logaggregator-mobileapp-uq|10.177.17.133|PASSWD|-|	
|EC2|prd01-a-vir-web-mobileapp-uq|10.177.19.232|PASSWD|-|	
|EC2|prd01-b-vir-web-mobileapp-uq|10.177.20.63|PASSWD|-|	
|ElastiCache|prd01-vir-mobileapp|-|-|-|	
|ElastiCache|prd02-vir-mobileapp|-|-|-|	
|ELB|prd01-vir-web-mobileapp-uq|-|-|-|	
|ELB|prd01-vir-api-mobileapp-uq|-|-|-|	
|RDS|prd01-vir-mobileapp-uq|-|-|-|

#### ・nrpe Command:

* nrpe Restart Command (※ when restart, execute the following this command from the monitoring server)
  /home/nnet/script/remote_nrpe_restart IP Address<br>
    「-i option OK? [n]: 」to display, Type a [y] and enter ※after execute this command、it will take some times.<br>
    「-i option OK? [n]: 」to display, if type a [n] then becomes cancel from this command.

* nrpe Start Command<br>
/home/nnet/nrpe/src/nrpe -d /home/nnet/nrpe/nrpe.cfg

Display the following messages after execute this command:<br> #/home/nnet/script/remote_nrpe_restart

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
■ ELB Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|BackendConnectionErrors<br>HTTPCode-5XX<br>HTTPCode-Backend-5XX<br>HealthyHostCount<br>UnHealthyHostCount|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email & phone contact|May_day|
|Latency|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|

■ RDS Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|CPU-Utilization<br>FreeStorageSpace<br>FreeableMemory<br>Health-check<br>SwapUsage|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|

■ ElastiCache Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|CPUUtilization-0001<br>FreeableMemory-0001<br>SwapUsage-0001|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|

■ EC2 Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|CPU-Utilization<br>DISK-/<br>Freeable-Memory<br>Swap-Usage|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact<br>※description of cause process is unnecessary to send by email|May_day|
|LOAD<br>iNode|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>※description of cause process is unnecessary to send by email<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|NTP-syncronization|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-CROND|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-MUNIN|No action required|/etc/rc.d/init.d/munin-node (stop/start/restart)|May_day|
|PROCS-SSH|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-SYSLOGD|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS-LOGSTASH|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|LOG-boot|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/boot/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/boot.log<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/boot/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-messages|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>※Point of note③ Contact is unnecessary when detected the target log is the log related to "ldap"<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/messages/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/messages<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/messages/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-secure|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>※Point of note③ If there is a recent email of autoscale add, and if IP of the recent email matches the server IP of alert detection, then Ack is executed and not necessary to contact the client. After Ack executed and after recovery return to normal operation.<br>◇Sample of email title of autoscale add:<br>{Server Name} AutoScale server is added!<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/secure/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/secure<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/secure/NGWRD-file<br>※lock file is not generated|May_day|
|LOG-spooler|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>Send the log contents by email, after that make a phone contact<br>cat /home/nnet/script/log-check/spooler/ANS-file<br>※check the error contents in the monitoring target log, because the error contents has been extracted<br>■ Monitoring target log check<br>/var/log/spooler<br>■ Sample string of the target monitored<br>※ refer to the following file<br>/home/nnet/script/log-check/spooler/NGWRD-file<br>※lock file is not generated|May_day|
|StatusCheckFailed-Instance|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|StatusCheckFailed-System|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact|May_day|
|uniqlo_api_error-LOG|No action required|■ email contact<br>◇Case of alert detection<br><br>・Alert detect more than 100 per hour<br><ERROR_API_NOT_FOUND><br><ERROR_AUTHKEY_INVALID><br><ERROR_NO_USER_DATA><br><ERROR_PARAMETER_UNDEFIND><br><ERROR_SESSION_INVALID><br><ERROR_HANDLING><br><br>・Not target alert<br><ERROR_APPVERSION_DISABLED><br><ERROR_DEVICETIME_INVALID><br><br>・Sequential alert (ERROR other than the above)<br><ERROR_*><br><br>■ Operation Procedure<br>email & phone contact|May_day|
|PROCS_td-agent
td-agent-SEND|No action required|/usr/lib64/fluent/ruby/bin/fluentd (stop/start/restart)<br>/etc/rc.d/init.d/td-agent (stop/start/restart)<br><br>■ Operation Procedure<br>contact email after above executed command|May_day|

## 4. How to Restart the Server
-----
##### ※ Follow the instruction of the AWS (Management Console) Restart Manual

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

To: uniqlo_alert_us@yumemi.in<br>
Cc: infra@mail.fastretailing.com<br>

■Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1|Ozeki San|090-7410-9075|
|2|Watanabe San|080-9279-5297|
|3|Fujikawa San|070-5554-5801|

----------------------------------



