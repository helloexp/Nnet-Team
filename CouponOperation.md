## Coupon Operation Manual

## Contents

1. Specific Remarks<br> 
2. Server List<br>
3. Operation Procedure<br>
4. How to Restart the Server<br>
5. Emergency Contact<br>
6. Submit to Troubleshooting Report

## 1. Specific Remarks

---------------------------------
* All alerts will be notified to clients by slack.
* It is necessary to contact even for alerts immediate   recovery. And if alerts are repeatedly detected and restored, then its continuous monitoring is OK. 
<br>
The following settings are necessary to browser of each Server and Nagios at this project.<br>
 * Required to VPN connection for FR project.

You are notified to customers via slack when alert occurs in all new infra projects, but if you receive a large amount of alerts then there may be need to inquiries to customers.

## 2. Server List
----
Tokyo Region Monitoring Server: mnt01-a-tky-nagios-common
----
| Down Work | Type | Server Name | Global IP | Local IP | Server Info | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|:----------:|
|※1|-|mnt01-a-tky-nagios-common|-|10.184.232.10|mnt01-a-tky-nagios-common server info|PASSWD|Monitoring Server|
|※2|EC2|prd01-a-tky-admin-coupon-fr|-|10.184.19.211|prd01-a-tky-admin-coupon-fr server info|PASSWD|-|
|※2|EC2|prd01-a-tky-batch-coupon-fr|-|10.184.18.126|prd01-a-tky-batch-coupon-fr server info|PASSWD|-|
|※2|EC2|prd01-a-tky-logaggregator-coupon-fr|-|10.184.16.107|prd01-a-tky-logaggregator-coupon-fr server info|PASSWD|-|
|※2|Elasticsearch Service|prd01-tky-es-coupon|-|-|-|-|-|
|※2|ASG|api-coupon-fr-IP-ADDRESS|-|-|-|-|-|

##### The following pattern of contact:<br>
「※1」 Mail contact + Phone contact + Restart event <br>
「※2」 Mail contact + Restart event <br>
「※3」 Request restart from  clients<br>
「※4」 Automatically monitoring delete. <br>When the new server is added for monitoring, check the email and it is confirmed,<br>If is not confirmed by email then setup manually the new instance for monitoring.

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
<br><br>

■ ELB Monitoring<br>

Monitoring server: mnt01-a-tky-nagios-common

|Host Name|Contents|Warning|Primary operation for Critical|Manually Check|
|:-----:|:-----:|:-----:|:----:|:----:|
|ELB_prd01-tky-admin-coupon-fr|ELB_Latency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-admin-coupon-fr|HTTPCode_Backend_5XX|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-admin-coupon-fr|HTTPCode_ELB_5XX|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-admin-coupon-fr|UnHealthyHostCount|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-api-coupon-fr|ELB_Latency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-api-coupon-fr|HTTPCode_Backend_5XX|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-api-coupon-fr|HTTPCode_ELB_5XX|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|ELB_prd01-tky-api-coupon-fr|UnHealthyHostCount|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|

■ RDS Monitoring<br>
Monitoring server (mnt01-a-tky-nagios-common)<br>

|Host Name|Contents|Warning|Primary Operation for Critical|Manually Check|
|:-----:|:-----:|:-----:|:----:|:----:|
|RDS_prd01-tky-enews-fr|BinLogDiskUsage|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|CPU_Utilization|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|FreeStorageSpace|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|FreeableMemory|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|Health check|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|ReadLatency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|SwapUsage|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr|WriteLatency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|BinLogDiskUsage|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|CPU_Utilization|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|FreeStorageSpace|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|FreeableMemory|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|Health check|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|ReadLatency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|SwapUsage|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|
|RDS_prd01-tky-enews-fr-read|WriteLatency|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required,<br>even in the case of immediate recovery, also there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day|

## 3. Operation Procedure
----
|Type|Monitoring Contents|Warning|Primary Operation for Critical|Procedure to manually check|Remarks|
|:-----:|:-----:|:------:|:------:|:------:|:------:|
|EC2|LOAD|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day||
|EC2|Swap Usage|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② Execute Ack after sending email|/home/nnet/libexec/check_swap -w 70% -c 50%||
|EC2|DISK_/|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■Operation Procedure<br>①e-mail contact<br>② Execute Ack after sending email|/home/nnet/libexec/check_disk -w 80% -c 80% -p /||
|EC2|CPU_Utilization|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day||
|EC2|Freeable Memory|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①e-mail contact<br>② Execute Ack after sending email|/home/nnet/script/check_mem.pl 90 90||
|EC2|NTP_syncronization|Same as Critical|(1)ntpd restart<br>/etc/rc.d/init.d/ntpd (stop/start/restart)<br>↓<br>(2)In case not recovery, change to ntp.conf server on the Amazon of ntp server then restart ntpd<br>after ntpd restart but not recovery then follow the next procedure:<br> ⇒ if rocovery, no action required<br> ⇒if not recovery, contact by email|May_day||
|EC2|LOG-apache|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>※ Point of note③ if the contents of log is「File does not exist」then no action required ■ operation Procedure<br>report to log contents by email<br>cat /home/nnet/script/log-check/apache/ANS-file<br>※ check the error log content have any monitoring target files are exist.<br>if the contents of log is「File does not exist」then no action required.<br><br>■ Target monitoring log<br>/var/log/httpd/error_log<br><br>■ Target monitoring sample file<br>/home/nnet/script/log-check/apache/NGWRD-file<br> ■ Phone Contact<br>not necessary|May_Day||
|EC2|LOG-cron|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>report to log contents by email<br>cat /home/nnet/script/log-check/cron/ANS-file<br>※ check the error log content have any monitoring target files are exist.<br><br>■ Target monitoring log<br>/var/log/cron<br><br>■ Target monitoring sample file<br>/home/nnet/script/log-check/cron/NGWRD-file<br> ■ Phone Contact<br>not necessary|May_Day||
|EC2|LOG-mail|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br> ■ operation Procedure<br>report to log contents by email<br>cat /home/nnet/script/log-check/maillog/ANS-file<br>※ check the error log content have any monitoring target files are exist.<br><br>■ Target monitoring log<br>/var/log/maillog<br><br>■ Target monitoring sample file<br>/home/nnet/script/log-check/maillog/NGWRD-file<br> ■ Phone Contact<br>not necessary|May_Day||
|EC2|LOG-spooler|No action required|■Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br> ■ operation Procedure<br>report to log contents by email<br>cat /home/nnet/script/log-check/spooler/ANS-file<br>※ check the error log content have any monitoring target files are exist.<br><br>■ Target monitoring log<br>/var/log/spooler<br><br>■ Target monitoring sample file<br>/home/nnet/script/log-check/spooler/NGWRD-file<br> ■Phone Contact<br>not necessary|May_Day||
|EC2|LOG-secure|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br> ■ operation Procedure<br>report to log contents by email<br>cat /home/nnet/script/log-check/secure/ANS-file<br>※ check the error log content have any monitoring target files are exist.<br><br>■ Target monitoring log<br>/var/log/secure<br><br>■ Target monitoring sample file<br>/home/nnet/script/log-check/secure/NGWRD-file<br> ■ Phone Contact<br>not necessary|May_Day||
|EC2|PROCS_CROND|No action required|/etc/rc.d/init.d/crond (stop/start/restart)<br><br>if recovery, after execute above command then report to related in internal team,<br> but if not recovery then report to client by email.|May_Day||
|EC2|PROCS_SSH|No action required|/etc/rc.d/init.d/sshd restart<br><br>if recovery, after execute above command then report to related in internal team,<br> but if not recovery then report to client by email.|May_Day||
|EC2|PROCS_SYSLOGD|No action required|/etc/rc.d/init.d/rsyslog (stop/start/restart)<br><br>if recovery, after execute above command then report to related in internal team,<br> but if not recovery then report to client by email.|May_Day||
|EC2|StatusCheckFailed_Instance|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day||
|EC2|StatusCheckFailed_System|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day||
|EC2|iNode|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>In the case of immediate recovery, even there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>② If detected the following this case to require to phone contact after sending email<br>====<br>Case ①: When the same alert is detected within 30 minutes from the received time of 1st Alert Mail (1)<br>Case ②: When received an alert mail (2)<br>=====<br>③ In the case contacted by phone, then again reply a email with mention phone message info by the email of ①.|May_day||
|Elasticsearch Service|Domain Status|No action required|email contact required<br>※ Domain Status alert has detected at prd 01-tky-es-coupon, to confirm by email.|/usr/local/nnetworks/nagios_ariake/script/check_es_state prd01-tky-es-coupon||
|Elasticsearch Service|Elasticsearch_Free_storage_space|No action required|email contact required (also email to required after recovery)<br>※not required to phone contact<br>when DISK capacity becomes high, then necessary to phone contact|May_day||

## 4. How to Restart the Server
-----
##### ※ Follow the instruction of the (AWS Management Console)  Restart Manual

Restart event is follow the "reboot" execute<br>
※Dont follow the stop/start  execute for restart event

If require to stop/start execute then escalate to related in-charge team and report current situation<br>

#### Check the following requires when executing the ELB detaching operation:<br>
 
1. Check and confirm the target server to remove from ELB on the AWS management console
2. Check access log of the server (/var/log/httpd/access_log),<br>
and Login each server to remove from ELB and confirm the access yes/no from the user.
3. If access is possible to execute of ELB detaching by the above procedure(2) then,<br>
Rollback ELB ⇒ Detaching operation is execute again

## 5. Emergency Contact
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and English template.
<br>
##### [By using Japanese and English email Template]

■Contact email address:

To:    <br>
Cc:    <br>

■Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1|||	 
|2|||

## 6. Submit to troubleshooting Report:
------

Not Necessary.

----------------------------------







