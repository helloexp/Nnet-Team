## MessagePF_US_GlobalEC_Monitoring_Manual

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
Monitoring Server: mnt01-a-vir-dxc-nagios-common　※To connect via the platform of step Server
----
| Type | Server Name | Local IP | PASSWD | Remarks |
| :-------:|:--------:|:-------:|:-------:|:-------:|
|EC2|mnt01-a-vir-dxc-nagios-common|10.177.211.247|PASSWD|Monitoring Server|	
|EC2|us-east-1_message_EC2_prd01-b-vir-delivery-controller-message-fr|10.177.22.223|PASSWD|-|	
|EC2|us-east-1_message_EC2_prd01-b-vir-jenkins-message-fr|10.177.23.201|PASSWD|-|	
|EC2|us-east-1_message_EC2_prd01-vir-api-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	
|EC2|us-east-1_message_EC2_prd01-vir-bzapi-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	
|EC2|us-east-1_message_EC2_prd01-vir-delivery-woker-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	
|EC2|us-east-1_message_EC2_prd01-vir-extraction-worker-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	|EC2|us-east-1_message_EC2_prd01-vir-immediate-delivery-worker-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	|EC2|us-east-1_message_EC2_prd01-vir-list-receipt-worker-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	
|EC2|us-east-1_message_EC2_prd01-vir-status-update-worker-message-fr-asg-【IP】|-|PASSWD|AutoScaling Server|	
|ElastiCache|us-east-1_message_ElastiCache_prd01-vir-message-001|-|-|-|
|ElastiCache|us-east-1_message_ElastiCache_prd01-vir-message-002|-|-|-|	
|ELB|us-east-1_message_ELB_prd01-vir-api-message-fr|-|-|-|	
|ELB|us-east-1_message_ELB_prd01-vir-bzapi-message-fr|-|-|-|
|RDS|us-east-1_message_RDS_prd01-vir-aurora-message-cluster|-|-|-|

#### nrpe Command:

* nrpe Restart Command (※ command execute the following in below command on the monitoring server)
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
-------

Monitoring Server: mnt01-a-vir-dxc-nagios-common

■ ELB Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|BackendConnectionErrors<br>HTTPCode-5XX<br>HTTPCode-Backend-5XX<br>HealthyHostCount<br>UnHealthyHostCount|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email & phone contact<br>※ In case of an alert due to execute job:<br>Send email with alert message of due to the job execution impact.<br>Phone contact is not required.|May_day|
|Latency|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact<br>※ In case of an alert due to execute job:<br>Send email with alert message of due to the job execution impact.<br>Phone contact is not required.|May_day|

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
|LOAD<br>iNode|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact<br>※description of cause process is unnecessary to send by email<br>②After email contact, if you face the following situation then make phone contact<br>=============<br>Case ①: When the same alert is detected again within 30 minutes from the reception of the first alert mail(1)<br>Case ②: When received the alert mail(2)<br>=============<br>③If you have made a phone call, please report with phone result by replying to first ①email to customer|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>email & phone contact<br>※description of cause process is unnecessary to send by email|May_day|
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
|PROCS_td-agent<br>td-agent-SEND|No action required|/usr/lib64/fluent/ruby/bin/fluentd (stop/start/restart)<br>/etc/rc.d/init.d/td-agent (stop/start/restart)<br><br>■ Operation Procedure<br>contact email after above executed command|May_day|

■ Individual Monitoring Items

|Target Server|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|:----:|
|prd01-b-vir-jenkins-message-fr|all-member-ids-jenkins-NOT-WORK,<br>extraction-jenkins-NOT-WORK,<br>messagebox-log-collect-jenkins-NOT-WORK,<br>messagebox-old-purge-NOT-WORK,<br>messagemaster-log-collect-jenkins-NOT-WORK,<br>messagemaster-old-purge-NOT-WORK,<br>status-update-jenkins-NOT-WORK,<br>timer-delivery-jenkins-NOT-WORK|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure:<br>email and phone contact<br><br>◇Alert detection condition◇<br>※ Detect alert, when job is not executed regularly every 2 minutes:<br>extraction-jenkins-NOT-WORK<br>timer-delivery-jenkins-NOT-WORK<br>status-update-jenkins-NOT-WORK<br>※etect alert, when job is not executed regularly every day:<br>messagebox_old_purge-NOT-WORK<br>messagebox_log_collect-jenkins-NOT-WORK<br>messagemaster_old_purge-NOT-WORK<br>messagemaster_log_collect-jenkins-NOT-WORK<br>Detect alert, when job is not executed regularly every 10 minutes:<br>all_member_ids-jenkins-NOT-WORK|May_day|
|us-east-1_message_EC2_prd01-vir-api-message-fr-asg-【IP】|HTTP<hr />apache-LOG|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure:<br>email and phone contact<hr />■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log <br>/var/log/httpd/error_log<br>■ Sample string of the target monitored<br>"response_code":500<br>■ lock file<br>/home/nnet/script/messagepf.lock|May_day|
|us-east-1_message_EC2_prd01-vir-status-update-worker-message-fr-asg-【IP】|PROCS_SUPERVISOR<br>PROCS_SUPERVISOR_CHILD_FATAL<hr />app-LOG-CRITICAL<br>app-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure:<br>email contact<hr />■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log <br>/var/log/app/message_timer_delivery_worker_app.log<br>■ Sample string of the target monitored<br>・app-LOG-CRITICAL<br>[CRITICAL]<br>・app-LOG-WARNING<br>[WARNING]<br>■ lock file<br>・app-LOG-CRITICAL<br>/home/nnet/script/log/appCRITICAL.lock<br>・app-LOG-WARNING<br>/home/nnet/script/log/appWARNING.lock|May_day|
|us-east-1_message_EC2_prd01-vir-extraction-worker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-delivery-woker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-immediate-delivery-worker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-list-receipt-worker-message-fr-asg-【IP】|PROCS_SUPERVISOR<br>PROCS_SUPERVISOR_CHILD_FATAL<hr />app-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure:<br>email and phone contact<hr />■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_timer_delivery_worker_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]<br>■ lock file<br>/home/nnet/script/log/appCRITICAL.lock|May_day|
|us-east-1_message_EC2_prd01-vir-extraction-worker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-delivery-woker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-immediate-delivery-worker-message-fr-asg-【IP】<br>us-east-1_message_EC2_prd01-vir-list-receipt-worker-message-fr-asg-【IP】|app-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log <br>/var/log/app/message_timer_delivery_worker_app.log<br>■ Sample string of the target monitored<br>[WARNING]<br>■ lock file<br>/home/nnet/script/log/appWARNING.lock|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-extraction-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_pack_controller_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_timer_delivery_controller_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|status-update-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_delivery_status_controler_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|old_message_purge-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_old_message_purge_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|log_collect-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_member_message_log_collect_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|all_member_ids-LOG-CRITICAL|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_pack_controller_all_member_ids_app.log<br>■ Sample string of the target monitored<br>[CRITICAL]|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-NO_DELIVERY_DATA|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email and phone contact<br>■ Monitoring target log <br>/var/log/app/message_delivery_status_controler_app.log<br>■ Sample string of the target monitored<br>TIMER_DELIVERY_NO_DELIVERY_DATA|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-extraction-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_pack_controller_app.log<br>■ Sample string of the target monitored<br>[WARNING]|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_timer_delivery_controller_app.log<br>■ Sample string of the target monitored<br>[WARNING]|May_day|
|prd01-b-vir-delivery-controller-message-fr|old_message_purge-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_old_message_purge_app.log<br>■ Sample string of the target monitored<br>[WARNING]|May_day|
|prd01-b-vir-delivery-controller-message-fr|log_collect-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_member_message_log_collect_app.log<br>■ Sample string of the target monitored<br>[WARNING]|May_day|
|prd01-b-vir-delivery-controller-message-fr|all_member_ids-LOG-WARNING|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_pack_controller_all_member_ids_app.log<br>■ Sample string of the target monitored<br>[WARNING]|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-DELAYED_EXTRACTION|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_delivery_status_controler_app.log<br>■ Sample string of the target monitored<br>EXTRACTION_PROCESS_IS_DELAYED|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-DELAYED_DELIVERY|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_delivery_status_controller_app.log<br>■ Sample string of the target monitored<br>DELIVERY_PROCESS_IS_DELAYED|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-LOW_EXTRACTION_RATE|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_delivery_status_controler_app.log<br>■ Sample string of the target monitored<br>EXTRACTION_RATE_IS_TOO_LOW|May_day|
|prd01-b-vir-delivery-controller-message-fr|timer-delivery-LOW_DELIVERY_RATE|No action required|■ Point of Notes<br>※ Point of note① contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, also even in the case of immediate recovery, and there is no need to mention restored<br>■ Operation Procedure:<br>Send the log contents by email<br>■ Monitoring target log<br>/var/log/app/message_delivery_status_controler_app.log<br>■ Sample string of the target monitored<br>DELIVERY_RATE_IS_TOO_LOW|May_day|


### 4. How to Restart the Server
-----
##### ※ Follow the instruction of the (AWS management Console based ) server Restart Manual

Restart event is follow the "reboot" execute<br>
※Dont follow the stop/start  execute for restart event

If a case require to stop/start execute then escalate to related in-charge team and report current situation<br>

####  Check the following requires when executing the ELB detaching operation:<br>
 
1. Check and confirm the target server to remove from ELB on the AWS management console
2. Check access log of the server (/var/log/httpd/access_log),<br>
and Login each server to remove from ELB and confirm the access yes/no from the user.
3. If access is possible to execute of ELB detaching by the above procedure(2) then,<br>
Rollback ELB ⇒ Detaching operation is execute again

## 5. Emergency Contact information
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and English template.
<br>
##### [By using Japanese and English mail Template]

■ Contact email address:<br>

To: uniqlo_alert@yumemi.in<br>
Cc: infra@mail.fastretailing.com<br>

■ Contact Phone: 

||Contact Name|Phone Number|
|:-----:|:-----:|:----:|
|1|藤川(Fujikawa)|070-5554-5801|	 
|2|渡邉(Watanabe)|080-9279-5297|
|3|大関(Ozeki)|090-7410-9075|	 
|4|阿部(Abe)|080-9423-1559|

----------------------------------



