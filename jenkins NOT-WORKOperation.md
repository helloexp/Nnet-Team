## jenkins NOT-WORK Alert Operation

## Contents

1. Specific Notes<br> 
2. Overview of Monitoring<br>
3. Jenkins window User/PW<br>
4. Jenkins job Stop Procedure<br>
5. Contact<br>

## 1. Specific Notes
--------------------

* When restarting Nagios with kill all command, the check interval may be reset and alert may be detected.<br>
In that case, check the status of the target job, and if confirmed that it is not failure, then take measures to reschedule the check at the appropriate time.

## 2. Overview of Monitoring
----

| Monitoring Contents | Overview of monitoring | Log File | jenkin Link | Primary operation |
| :----------:|:------------:|:------------:|:------------:|:------------:|
|storecms-sync-recruit-NOT-WORK|If the log doesnt increase 2 times in the past 90 minutes, then detect alert|/var/lib/jenkins/jobs/prd01-store_sync_recruit/builds/*/log|[Jenkins Login](http://10.184.17.248:8080/login?from=%2Fjob%2Fprd01-store_sync_recruit%2F)|Stop the jenkins jobs if that take time|
|ftp-cleanup-NOT-WORK|If the log doesnt increase 2 times in the past 3 hours, then detect alert|/mnt/jobs/yumemi_Production_Storecatalog_inventory-ftp_cleanup/builds/*/log|[Jenkins Login](http://10.184.19.163:8080/login?from=%2Fjob%2Fyumemi_Production_Storecatalog_inventory-ftp_cleanup%2F)|Stop the jenkins jobs if that take time|
|sales-ftp-cleanup-NOT-WORK|If the log doesnt increase 2 times in the past 60 minutes, then detect alert|/mnt/jobs/yumemi_Production_Storecatalog_sales-ftp_cleanup/*/log|[Jenkins Login](http://10.184.19.163:8080/login?from=%2Fjob%2Fyumemi_Production_Storecatalog_sales-ftp_cleanup%2F)|Stop the jenkins jobs if that take time|
|storelist-upload-NOT-WORK|If the log doesnt increase 4 times in the past 30 minutes, then detect alert|/mnt/jobs/prd11-storecatalog_batch_upload-store-list/builds/*/log|[Jenkins Login](http://10.184.19.163:8080/login?from=%2Fjob%2Fprd11-storecatalog_batch_upload-store-list%2F)|Stop the jenkins jobs if that take time|
|extraction-jenkins-NOT-WORK|If the log doesnt increase 3 times in the past 10 minutes, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_produce-extraction-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_produce-extraction-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|timer-delivery-jenkins-NOT-WORK|If the log doesnt increase 3 times in the past 10 minutes, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_produce-delivery-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_produce-delivery-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|status-update-jenkins-NOT-WORK|If the log doesnt increase 3 times in the past 10 minutes, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_update-delivery-status-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_update-delivery-status-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|messagebox_old_purge-NOT-WORK|If the log increases less than 1 time per day, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_messagebox_delete-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_messagebox_delete-uqapp_jp)|Stop the jenkins jobs if that take time|
|messagebox_log_collect-jenkins-NOT-WORK|If the log increases less than 1 time per day, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_messagebox_log_collect-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_messagebox_log_collect-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|messagemaster_log_collect-jenkins-NOT-WORK|If the log increases less than 1 time per day, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_messagemaster_log_collect-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_messagemaster_log_collect-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|messagemaster_old_purge-NOT-WORK|If the log increases less than 1 time per day, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_messagemaster_delete-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_messagemaster_delete-uqapp_jp%2F)|Stop the jenkins jobs if that take time|
|all_member_ids-jenkins-NOT-WORK|If the log increases less than 1 time per day, then detect alert|/var/lib/jenkins/jobs/prd01-message_controller_pack_all_member_tsv-uqapp_jp/builds/*/log|[Jenkins Login](http://10.184.20.107:8080/login?from=%2Fjob%2Fprd01-message_controller_pack_all_member_tsv-uqapp_jp)|Stop the jenkins jobs if that take time|

## 3. Jenkins Login window ID/PW

Click the Jenkins Login and fill in the User and Password.<br>
User: ............<br>
Password: ...............

## 4. job Stopping Procedure

Check and confirm the jenkins running from the jenkins build history and click stop jenkins jobs.

## 5. Contact

If failure or stop jenkins jobs-<br>
Contact to email to related team and report current situation.<br>

■Contact email address:

To:    <br>
Cc:    <br>

-----------------------
