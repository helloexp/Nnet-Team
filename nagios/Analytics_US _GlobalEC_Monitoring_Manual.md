
## Analytics(MDWH)_US_GlobalEC_Monitoring_Manual

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
Monitoring Server: mnt01-a-vir-dxc-nagios-common<br>※To connect via the platform of step Server

| Type | Server Name | Local IP | PASSWD | Remarks |
| :-------:|:-------:|:-------:|:--------:|:-------:|
|EC2|mnt01-a-vir-dxc-nagios-common|10.177.211.247|PASSWD|Monitoring server|	
|EC2|prd01-a-vir-batch-mdwh-uniqlo|10.177.19.225|PASSWD|-|	
|EC2|prd01-b-vir-batch-mdwh-uniqlo|10.177.23.22|PASSWD|-|	
|EC2|prd01-a-vir-step-mdwh-uniqlo|10.177.19.178|PASSWD|-|	
|EC2|prd01-a-vir-jenkins-mdwh-uniqlo|10.177.16.19|PASSWD|-|	
|Redshift|redshift.mdwh.us.fastretailing.com|10.177.25.96|-|Redshift, allow no login|	
|Redshift|Redshift_prd01-vir-mdwh.cl7ljcnhjch4.us-east-1.redshift.amazonaws.com|-|-|Redshift, allow no login|	

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
---
■ Redshift Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:----:|:----:|
|CPUUtilization_Compute-0<br>CPUUtilization_Compute-1<br>HealthStatus_Compute-0<br>HealthStatus_Compute-1<br>PercentageDiskSpaceUsed_Compute-0<br>PercentageDiskSpaceUsed_Compute-1<br>HealthStatus_Leader|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required.<br>even in the case of immediate recovery, there is no need to mention restored.<br><br>■ Operation Procedure<br>①email contact|May_day|

■ EC2 Monitoring

|Items Name|Warning|Critical|Manual Check|
|:-----:|:-----:|:-----:|:----:|
|CPUUtilization|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br>■ Operation Procedure<br>①email contact※d escription of cause process is unnecessary to send by email|May_day|
|LOAD|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br><br>■ Operation Procedure<br>①email contact|May_day|
|NTP_syncronization|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br><br>■ Operation Procedure<br>①email contact|May_day|
|Swap Usage|No action required|■ Point of Notes<br>※ Point of note① email contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br><br>■ Operation Procedure<br>①email contact|May_day|
|PORT_8080|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br><br>■ Operation Procedure<br>①email contact|May_day|
|DISK_/|No action required|■ Point of Notes<br>※ Point of note① mail contact required even for immediate recovery<br>※ Point of note② recovery contact is not required, even in the case of immediate recovery, there is no need to mention restored<br><br>■ Operation Procedure<br>①email contact<br>②execute Ack after email contact|May_day|

## 4. How to Restart the Server
-----
#### Follow the instruction of the (AWS management console) server Restart Manual

Restart event is follow the "reboot" execute<br>
※ Dont follow the stop/start execute for restart event

In the case of require to stop/start execute then escalate to related in-charge team and report current situation<br>

### Check the following requires when executing the ELB detaching operation:<br>
 
1. Check and confirm the target server to remove from ELB on the AWS management console
2. Check access log of the server (/var/log/httpd/access_log),<br>
and Login each server to remove from ELB and confirm the access yes/no from the user.
3. If access is possible to execute of ELB detaching by the above procedure(2) then,<br>
Rollback ELB ⇒ Detaching operation is execute again

## 5. Emergency Contact Information
---
Contact and send email to person in charge found from contact list in triage sheet by using Japanese and English template.
<br>
##### [By using Japanese and English email Template]

■ Contact email address:

To: daiki.shimozono@fastretailing.com, 
fahima.rahim@fastretailing.com, ACN_FR_AnalyticsPlatform@accenture.com<br>
Cc: dxc@    <br>

■ Contact Phone: 
If have any major problems or troubles & need to escalate then contact to person in charge of Operation Team.<br>

||Contact Name|Phone No.|
|:-----:|:-----:|:----:|
|1|N/A|N/A|	 

----------------------------------



