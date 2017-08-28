
## MDWH Operation Manual

## Contents

1. Specific Remarks<br> 
2. Server List<br>
3. Operation Procedure<br>
4. How to Restart the Server<br>
5. Emergency Contact<br>
6. Submit to Troubleshooting Report

## 1. Specific Remarks

---------------------------------
  * Point of notes when delete monitoring..   
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
Monitoring Server: mnt01-a-vir-nagios-common　※To connect via the platform of Bastion Server
----
| Down Work | Server Name | Global IP | Local IP | Server Info | PASSWD | Remarks |
| :----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|
|※1	|mnt01-a-vir-nagios-common	|-	|10.177.209.194	|mnt01-a-vir-nagios-common server info|PASSWD|monitoring server|
|※2	|prd01-a-vir-batch-mdwh-uniqlo	|-	|10.177.19.225	|prd01-a-vir-batch-mdwh-uniqlo info|PASSWD||	
|※2	|prd01-b-vir-batch-mdwh-uniqlo	|-	|10.177.23.22	prd01-a-vir-batch-mdwh-uniqlo info|PASSWD||	
|※2	|prd01-a-vir-step-mdwh-uniqlo	|-	|10.177.19.178	|prd01-a-vir-step-mdwh-uniqlo server info|PASSWD||	
|※2	|prd01-a-vir-jenkins-mdwh-uniqlo	|-	|10.177.16.19	|prd01-a-vir-jenkins-mdwh-uniqlo server info|PASSWD||	
|※2	|redshift.mdwh.us.fastretailing.com	|-	|10.177.25.96	|-|-|Redshift、allow no login|
|※2	|Redshift_prd01-vir-mdwh.cl7ljcnhjch4.us-east-1.redshift.amazonaws.com|-|-|-|-|Redshift、allow no login|


The following pattern of contact of the clients:<br>
「※1」 Mail contact + Phone contact + Restart event <br>
「※2」 Mail contact + Restart event <br>
「※3」 Request restart<br>
「※4」Automatically delete monitoring, The new server is         added and monitored then confirmed to notify      e-mail.<br>If it do not confirm e-mail then the new instance manually added monitor.

#### nrpe Command:

* nrpe Restart Command (※ command execute the following in below command from the monitoring server)
  /home/nnet/script/remote_nrpe_restart IP Address<br>
    「-i option OK? [n]: 」to display, Type a [y] and enter ※after execute this command、it will take some times.<br>
    「-i option OK? [n]: 」to display, if type a [n] then becomes cancel from this command.

* nrpe Start Command<br>
/home/nnet/nrpe/src/nrpe -d /home/nnet/nrpe/nrpe.cfg

#### Sample event of after execute this command:<br> 
#/home/nnet/script/remote_nrpe_restart

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
■Redshift monitoring

|Contents|Warning|Critical on first time operation|Manual Check|
|:-----:|:-----:|:----:|:----:|
|CPUUtilization_Compute-0<br>CPUUtilization_Compute-1<br>HealthStatus_Compute-0<br>HealthStatus_Compute-1<br>PercentageDiskSpaceUsed_Compute-0<br>PercentageDiskSpaceUsed_Compute-1<br>HealthStatus_Leader|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>even in the case of immediate recovery, there is no need to mention restored.<br><br>■Operation Procedure<br>①e-mail contact|May_day|

■EC2 Monitoring

|Type|Monitoring Contents|Warning|First time operation for Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|:----:|
|EC2|CPUUtilization|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br>■Operation Procedure<br>①e-mail contact|May_day|
|EC2|LOAD|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br><br>■Operation Procedure<br>①e-mail contact|May_day|
|EC2|NTP_syncronization|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br><br>■Operation Procedure<br>①e-mail contact|May_day|
|EC2|Swap Usage|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br><br>■Operation Procedure<br>①e-mail contact|May_day|
|EC2|PORT_8080|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br><br>■Operation Procedure<br>①e-mail contact|May_day|
|EC2|DISK_/|No action required|■Notes<br>※ Point of note① mail contact required for immediate recovery<br>※ Point of note② recovery contact is not required.<br>Even in the case of immediate recovery, there is no need to mention restored<br><br>■Operation Procedure<br>①e-mail contact|May_day|

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



