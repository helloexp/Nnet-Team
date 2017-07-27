                                             Influencer Operation Manual
test epilepil
##### Contents

1 Specific Remarks<br> 
2 Server List<br>
3 Operation Method<br>
4 How to restart the server<br>
   
    4.1 Emergency Contact
    4.2 Troubleshooting Report Submit

## Specific Remarks

---------------------------------
  * Remember below points when delete on monitoring   
     * Dont forget delete on Munin setup
     * If you contact regarding the deleted server and if there has a alert, also please close its.<br>

----

The following settings are necessary to browser of each server and nagios at this project.<br>

 * Need to VPN connection of FR project.

When there are many connections from the following IP and its connected from related server of FAST RETAILING, do not set refusal, just you will inform to FR that connection is load from target IP.

■ Excluded Target IP

54.199. *. *<br>
※If other exclusion IPs are increase, please correction the above list with all wiki of FAST RETAILING.

## Server List:
----
Monitoring Server: mnt01-a-tky-nagios-common　※Via the platform of Step Server

----
|Down Work|Server Name|Global IP|Local IP|Server Info|PASSWD|Remarks|
|:----------:|:------------:|:------------:|:------------:|:------------:|:----------:|:----------:|
|※2|mnt01-a-tky-gateway-common|54.250.223.60|10.184.192.6|mnt01-a-tky-gateway-common server info|PASSWD|Step platform Server|
|※2|mnt01-a-tky-nagios-common|-|10.184.232.10|mnt01-a-tky-nagios-common Server info|PASSWD|Monitoring Server|
|Still Watching|Influencer-[IP]|-|-|-|PASSWD|AutoScaling Server
|※2|prd01-a-tky-batch-influencer-uniqlo|-|10.184.17.46|prd01-a-tky-batch-influencer-uniqlo server info|PASSWD|-|
|※2|prd01-a-tky-admin-influencer-uniqlo server info|-|10.184.17.202|prd01-a-tky-admin-influencer-uniqlo server info|PASSWD|-|	
|※2|RDS_prd01-tky-influencer-uniqlo|-|-|-|-|RDS:<br> no Login| 
|※2|RDS_prd01-tky-influencer-uniqlo-read|-|-|-|-|RDS: <br>No Login|
   
The following contact of client:<br>
「※1」 Mail contact + Phone contact + Restart event <br>
「※2」 Mail contact + Restart event <br>
「※3」 Request to Restart 

nrpe Command:

* nrpe Restart Command(※Please its implement the following in below command from Monitoring Server)
  /home/nnet/script/remote_nrpe_restart IP Address<br>
    「-i option OK? [n]: 」to display, Type a [y] and enter ※after execute、it will take some times.<br>
    「-i option OK? [n]: 」to display, if you type a [n] then becomes cancel.

* nrpe Start Command<br>
/home/nnet/nrpe/src/nrpe -d /home/nnet/nrpe/nrpe.cfg

■URL Monitoring<br>
Monitoring server: mnt01-a-tky-nagios-common <br>
※Via the platform of step server

|Monitoring Contents|URL|Remarks|During the first time operation but not yet recovered|
|:-----:|:-----:|:-----:|:------:|
|SSL_lifewear.uniqlo.com_people_people_jeans|https://lifewear.uniqlo.com/people/jeans|End user reference page status code 「200」 is OK, <br>Restart the nginx of the target ELB on the following server|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|
|SSL_lifewear.uniqlo.com_people_form_ja|https://lifewear.uniqlo.com/form/ja|End user reference page status code 「401」 is OK, <br>Restart the nginx of the target ELB on the following server|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|
|SSL_lifewear.uniqlo.com|https://lifewear.uniqlo.com/status.html|Influencer reg. display status code 「200」 is OK,<br>Restart the nginx of the target ELB on the following server|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|
|SSL_admin-lifewear.uniqlo.com|https://admin-lifewear.uniqlo.com/status.html|Administrator authority display status code 「200」 is OK, <br>Restart the nginx of the target ELB on the following server|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|

■URL Monitoring (ELB）<br>
Monitoring Server: mnt01-a-tky-nagios-common <br>
※Via of step platform Server ※When finding ELB, attention by inflencr and influencer.

----

|Object HOST|URL|Way to First time operation|Way to manually check|During the first time operation but not yet recovered|
| :----------:| :------------: |:------------:|:------------:|:----------: |
|ELB_prd01-tky-admin-inflencr-uniqlo-elb.amazonaws.com|https://prd01-tky-admin-inflencr-uniqlo-1751200015.ap-northeast-1.elb.amazonaws.com/status.html|Restart the nginx of the target ELB on following server|May_Day|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|
|ELB_prd01-tky-influencer-uniqlo-elb.amazonaws.com|http://prd01-tky-influencer-uniqlo-304455623.ap-northeast-1.elb.amazonaws.com/status.html|Restart the nginx of the target ELB on following server|May_Day|※After first time operation and recover can not be confirmed and<br> if there is impact in service then follow this reference|

Operation Method
---
|Monitoring Contents|Way to first time operation/Command|Way to manually check|
|:-----:|:-----:|:------:|
|DOWN <br>SSH|Server restart|May_Day|
|DOWN ※multiple servers※|When the multiple servers of FR are DOWN then follow the way to operation work|Ping check from the monitoring server<br>and status check from the AWS management console|
|CPU|If there is no impact on other monitoring contents please contact email with the cause of the load,<br>If there is an impact on other monitoring contents then do work operation|/home/nnet/script/check_cpu 80 90|
|HTTP|・Check the nginx process following the command:<br>ps aux grep unicorn<br>ps aux grep nginx<br>・If have no exist process then do start the process following this manual.<br>* In case of unicorn ⇒ PROCS_unicorn_rails<br>*In case of nginx ⇒ Implement URL|May_Day|
|URL* <br>SSL* <br>ELB*|/etc/rc.d/init.d/nginx (stop/start/restart)<br>・Check the process in below command:<br>ps aux grep  nginx<br>----------------------------------<br>root 10349 0.0 0.0 109464 2164 ? Ss 07:44 0:00 nginx: master process<br> /usr/sbin/nginx -c /etc/nginx/nginx.conf nginx 10350 0.0 0.0 109828 3292 ? S 07:44 0:00 nginx: worker process<br>------------------------<br>* two processes are display depends on the setting.<br> ・Normally Web check<br>Check that each URL can be displayed normally and there is a ok response of 200.<br>※ If you can not confirm the recovery even after first opertation and if there is an impact on the service then follow this reference|May_Day|
|LOAD|If there is no impact on other monitoring contents please contact by email with the cause of the load<br>If there is an impact on other monitoring contents then do the operation work.|/home/nnet/libexec/check_load -w 5,10,15 -c 10,15,20|
|NTP|(1) ntpd restart /etc/rc.d/init.d/ntpd (stop/start/restart)<br>↓<br>(2) if not recovery、Changing the destination server of ntp.conf to amazon's ntp server then again restart ntpd, <br>After restart to ntpd: <br>⇒ if recovery,no need any other action <br> ⇒ if not recovery, then contact by email|/home/nnet/script /check_ntp|
|MYSQL<br>MYSQL_REP|Host: case of RDS: <br>Contact to phone<br> Contact: Normal contact+Specific responsibility person|MayDay|
|SWAP|After restart or stop of cause process then contact by email|/home / nnet / libexec / check_swap - w 70% - c 50%|
|DISK_ /|contact by email of current usage|/home/nnet/libexec/check_disk -w 30% -c 30% -p /<br>【prd01-a-tky-admin-influencer-uniqlo】<br>/home/nnet/libexec/check_disk -w 25% -c 20% -p /|
|PROCS_CROND|/etc/rc.d/init.d/crond (stop/start/restart) after execute above the command <br>if its recovery then contact to internal email in below: <br>To: syougai-ml@nnetworks.co.jp <br>Bcc: maintrance@nnetworks.co.jp <br>If its not recovery then contact to client by email|May_day|
|PROCS_SYSLOGD|/etc/rc.d/init.d/rsyslog (stop/start/restart) after execute above the command <br> if its recovery then contact to internal email in below: <br>To: syougai-ml@nnetworks.co.jp <br>Bcc: maintrance@nnetworks.co.jp <br>If its not recovery then contact to client by email|May_day|
|PROCS_munin|/etc/rc.d/init.d/munin-node (stop/start/restart) after execute above the command<br> if its recovery then contact to internal email in below: <br>To: syougai-ml@nnetworks.co.jp <br>Bcc: mailtrance@nnetworks.co.jp<br> If its not recovery then contact to client by email|May_day|
|PROCS_nginx|Start to nginx on URL followed by the restart manual<br>Nginx document root:<br>/usr/share/nginx/html/<br>After execute by above the command, if its not recovery then contact to client by the phone|/home/nnet/libexec/check_procs -c 1:1 -a "/usr/sbin/nginx -c /etc/nginx/nginx.conf"|
|PROCS_unicorn_rails|	・switch to www user by below command<br>su - www<br>cd /var/rails/influencer/current/<br>・To execute by below command<br>bundle exec unicorn_rails -c ./config/unicorn.rb -E production -D<br>process check by the below command<br>ps aux grep unicorn<br><br>■process example<br>------------------------------<br><br>www 7658 22.5 2.7 448308 111384 ? Sl 07:39 0:01 unicorn_rails master -c ./config/unicorn.rb -E production -D<br>www 7662 0.0 2.6 448176 105924 ? Sl 07:39 0:00 unicorn_rails worker[0] -c ./config/unicorn.rb -E production -D<br>www 7671 0.0 2.6 448320 105976 ? Sl 07:39 0:00 unicorn_rails worker[1] -c ./config/unicorn.rb -E production -D<br>---------------------------------<br>※10 to 20 processes exist depends on the setting<br><br>※ If its not recovery even after execute by the above manual then contact to client|/home/nnet/libexec/check_procs -c 1:1 -a "unicorn_rails mas|
|PROCS_TwitterStreamingDaemon_run|◇prd01-a-tky-batch-influencer-uniqlo server only<br>・check the process by the the below command<br>ps aux  grep TwitterStreamingDaemon<br><br>■process example<br>---------------------------<br>www 2177 0.5 2.1 400296 84400 ? Sl 07:19 0:01 <br>/usr/local/rbenv/versions/2.2.5/bin/ruby bin/rails runner TwitterStreamingDaemon.run run<br>-----------------------------<br><br>・In case processes are not exist,<br>・switch to www user by using this command:<br>su - www<br>execute this command:<br>cd /var/rails/influencer/script/sns<br>./twitter_stream.sh<br>------------------------<br>2015/3/27/Friday 08:04:05 UTC :{result:twitter_daemon_proc: running [pid 14397]}<br>-------------------------------<br>※ this is normal if the above process ID are displayed<br>・again check the process using below command:<br>ps aux  grep TwitterStreamingDaemon<br>■process example<br>--------------------------------<br><br>www 2177 0.5 2.1 400296 84400 ? Sl 07:19 0:01<br>/usr/local/rbenv/versions/2.2.5/bin/ruby bin/rails runner TwitterStreamingDaemon.run run<br>---------------------------------<br>※if process is normally started then OK<br><br>After execute by above the command, if its not recovery then contact to client|/home/nnet/libexec/check_procs -c 1:1 -a "twitter_daemon_proc"|
|CPU Utilization|email contact to client|MayDay|
|FreeStorageSpace|the current usage status notify by email<br>Storage check manual on the AWS management Console|MayDay|
|SlowQuery|inform by email that slow query count is incrementing continuously for 10 minutes in target RDS|MayDay|

How to Restart the server
-----
Server restart Manual of AWS Infrastructure ※Region of Tokyo

[AWS Restart Manual](http://192.168.1.20:81/index.php/AWS新基盤系サーバ再起動マニュアル)

Restart action is called the "reboot"<br>
※Dont restart by stop/start

If a case requiring unavoidably stop/start has occur then escalation with CEO.<br>

* Check the following requires when executing the ELB detaching work.<br>
 1. Check the target server to disconnect from ELB at the AWS side (Management Console, etc.)
 2. Check from the server access log (/var/log/httpd/access_log),<br>
 and Log in each server to separated from ELB and confirm regarding is access yes/not<br> from the user.
 3. If access is possible to execute of ELB detachment by the above procedure(2), <br>
   Rollback ELB ⇒ Detaching operation is execute again

AWS Emergency Contact
---
Please the following FR mail template of contents for email both in Japanase and english in details below: <br>
[FR Mail Template](http://192.168.1.20:81/index.php/FR_メールテンプレート)

■Contact email address

To:    uniqlo@ruby-dev.jp<br>
Cc:    infra@mail.fastretailing.com<br>
Bcc:  maintenance@nnetworks.co.jp

■Contact Phone 

||Contact Name|Contact No|
|:-----:|:-----:|:----:|
|1|Ruby Devp.|03-3527-3960 
|2|Ruby Devp.|03-3527-3962|
|3|Shibata|090-3417-7007<br>(After PM18 at night and holidays)|
|4|CEO|	080-4138-5222 
|5|Nishino|090-1657-2317|

Troubleshooting Report Submit:
--------------------

Not Necessary.

----------------------------------



