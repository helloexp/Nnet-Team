
## OrderPlatform Operation Manual

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

## 2. Server List:
----
Monitoring Server: mnt01-a-tky-nagios-common　※To connect via the platform of Bastion Server
----
| Down Work | Server Name | Global IP | Local IP | Server Info | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|
|※2|mnt01-a-tky-gateway-common|54.250.223.60|10.184.192.6|mnt01-a-tky-gateway-common server info|PASSWD|Bastion platform Server|
|※2|mnt01-a-tky-nagios-common|-|10.184.232.10|mnt01-a-tky-nagios-common Server info|PASSWD|Monitoring Server|
|※2|prd01-a-tky-nodejsapi-order|-|10.184.19.238|prd01-a-tky-nodejsapi-order server info|PASSWD|Order Api Server Monitoring autoscale AMI instance base, so it may be unnecessary to monitor?|
|※2|prd11-a-tky-adminapp-order|-|10.184.19.14|prd11-a-tky-adminapp-order server info|PASSWD||
|※2|prd11-a-tky-nodejsapi-order|-|10.184.18.131|prd11-a-tky-syncapi-order server info|PASSWD||	
|※2|prd11-a-tky-syncapi-order|-|10.184.17.141|prd11-a-tky-syncapi-order server info|PASSWD|| 
|※2|transaction_id-index|-|-|-|-|Dynamo DB Tables and Index|
|※2|Dynamo_DB_prd11_orderpf_delete_order|-|-|-|-|Dynamo DB Tables and Index|
|※2|Dynamo_DB_prd11_orderpf_hemmings_order|-|-|-|-|Dynamo DB Tables and Index|
|※2|Dynamo_DB_prd11_orderpf_order_transaction|-|-|-|-|Dynamo DB Tables and Index|
|※2|RDS_prd01-tky-order-fr|-|-|-|-|RDS:Allow no login|
|※2|prd11-tky-es-order-pf|-|-|-|-|Elasticsearch Service|
|Monitoring observation|prd11-worker-order-pf|-|-|-|-|Elastic BeanStalk Worker<br>AutoScaling server group|
|Monitoring observation|OrderPF_nodejsapi_[IP]|-|-|-|AutoScaling|
|Monitoring observation|OrderPF-nodejsapi-order_[IP]|-|-|-|AutoScaling server group|
|Monitoring observation|OrderPF_zipapi_[IP]|-|-|-|AutoScaling server group|
|Monitoring observation|OrderPF_indexingapi_[IP]|-|-|-|AutoScaling server group|

The following pattern of contact of the clients:<br>
「※1」 Mail contact + Phone contact + Restart event <br>
「※2」 Mail contact + Restart event <br>
「※3」 Request restart

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


## 3. Operation Procedure
---
|Monitoring Contents|Procedure to first time operation/Command|Procedure to manually check<br>：/usr/local/nnetworks/nagios_ariake/libexec|Remarks|
|:-----:|:-----:|:------:|:------:|
|CPUUtilization|WARNING<br>to report current usage by mail<br>CRITICAL<br>to report current usage by mail & phone|May_Day||
|CPUUtilization_80|to report current usage by mail|May_Day||
|CPUUtilization_85_95|WARNING<br>to report current usage by mail<br>CRITICAL<br>to report current usage by mail & phone|May_Day||
|Disk_/|WARNING<br>to report current usage by mail<br>CRITICAL<br>to report current usage by mail & phone|/home/nnet/libexec/check_disk -w 40% -c 10% -p /||
|ConsumedReadCapacityUnits_90|current usage report by mail & phone|May_Day||
|ConsumedReadCapacityUnits_95_97|WARNING<br>to report current usage by mail<br>CRITICAL<br>current usage report by mail & phone|May_Day||
|ConsumedWriteCapacityUnits_90|current usage report by mail|May_Day||
|ConsumedWriteCapacityUnits_45|current usage report by mail|May_Day||
|ConsumedWriteCapacityUnits_95_97|WARNING<br>current usage report by mail<br>CRITICAL<br>to report current usage by mail & phone|May_Day||
|EB_STATUS|WARNING<br>no need action<br>CRITICAL<br>health status check on the AWS management<br>WARNING if (warning) no need to contact<br>CRITICAL if (Critical) contact to phone<br>If its repeatedly detecting and recovering then contact to mail<br>UNKNOWN<br>①contact to specefic team<br>report to contact with alert title<br>②UNKNOWN<br>If the status last more than 30 minutes the escalate to specific team<br>※|May_Day||
|Network_IN|WARNING<br>current status report by mail<br>CRITICAL<br>current status report by mail & phone<br>|May_Day||
|StatusCheckFailed|current status report by mail|May_Day||
|StatusCheckFailed_CRITICAL|WARNING<br>current status report by mail<br>CRITICAL<br>current status report by mail & phone|May_Day||
|CPU|current value report from listed in Additional Info|May_Day||
|STORAGE|current value report from listed in Additional Info|May_Day||
|Domain Status|mail contact<br>※when do first time operation not need to check on the management display,<br>mail contact follow this comments: Domain Status alert was detected with prd11-tky-es-order-pf|/usr/local/nnetworks/nagios_ariake/script/check_es_state prd11-tky-es-order-pf||
|Elasticsearch_Free_storage_space|mail contact|May_Day||

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
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and english template.
<br>
##### [By using Japanese and english mail Template]

■Contact email address:

To:    <br>
Cc:    <br>

■Contact Phone: 

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1||	 
|2|||

## 6. Submit to troubleshooting Report:
------

Not Necessary.

----------------------------------



