vsdfgfsdfgsrtygrwer testimport os

DEFAULT_INDEX = 'Home'

def create_index():
    """ Creates an HTML index page to redirect to an MkDocs generated page. """
    html_code = \eftgherhger
        "<!DOCTYPE HTML>\n " \
        "<html>\n" \
        "\t<head>\n" \
        "\t\t<meta charset=\"UTF-8\">\n" \
        "\t\t<meta http-equiv=\"refresh\" content=\"1;url=%s/index.html\">\n" \
        % DEFAULT_INDEX + \
        "\t\t<script type=\"text/javascript\">\n" \
        "\t\t\twindow.location.href = \"%s/index.html\"\n" % DEFAULT_INDEX +\
        "\t\t</script>\n" \
        "\t</head>\n" \
        "\t<body>\n" \
        "\t\tIf you are not redirected automatically to the " \
        "%s page, follow this <a href=\"%s/index.html\">link</a>\n"\
        % (DEFAULT_INDEX, DEFAULT_INDEX) + \
        "\t</body>\n" \
        "</html>\n"

    print("Creating the index.html file...\n")
    generated_site_dir = os.path.join(MKDOCS_DIR, "site", "index.html")
    index_file = open(generated_site_dir, "w")
    index_file.write(html_code)
    index_file.close()


--------------------/ Staging_Blue SystemT/———————————————————————
  
## Staging SystemTest ( copy from GU Production) 
  
### DB1 ( Non Multi AZ )
  - DBInstanceIdentifier :stg01-tky-db-plm-gu-syst
  - Endpoint : stg01-tky-db-plm-gu-syst.chjlgx48usw9.ap-northeast-1.rds.amazonaws.com:1433
  - MasterUser/Pass:rdsmaster/Do0eAJkaYvI　　
  - InstanceType: db.r3.xlarge
  - OS: SQL Server 2014 SE
  
### DB2 ( Multi AZ )
  - DBInstanceIdentifier :stg02-tky-db-plm-gu-syst
  - Endpoint : stg02-tky-db-plm-gu-syst.chjlgx48usw9.ap-northeast-1.rds.amazonaws.com:1521
  - MasterUser/Pass:administrator/VXWwsJuMfg0　　
  - InstanceType: t2.medium
  - OS: SQL Server 2014 SE  
  
### AP1 Server
  - Name:stg01-a-tky-web-plm-gu-syst
  - InstanceType: m4.xlarge
  - InstanceID: i-0d9e592b2813e9208　　　
  - IP:10.184.83.25
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/2w;aYh3xPa
  - Hostname : SAP01PLM-GU-SYS  　

### AP2 Server
  - Name:stg02-c-tky-web-plm-gu-syst
  - InstanceType: m4.xlarge
  - InstanceID: i-08b0f78f7ac469945　　　
  - IP:10.184.87.140
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/(%-D?8D$;k!
  - Hostname : SAP02PLM-GU-SYS 

### PDF1 Server
  - Name:stg01-a-tky-pdf-plm-gu-syst
  - InstanceType: t2.large
  - InstanceID: i-077543c79ca3a2844　　　
  - IP:10.184.81.46
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/sCey2ReZd%
  - Hostname : SPDF01PLM-GU-S  　

### PDF2 Server
  - Name:stg02-c-tky-pdf-plm-gu-syst
  - InstanceType: t2.large
  - InstanceID: i-0528c4e5ed275d536　　　
  - IP:10.184.85.50
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/PpA&=KCn3WZ
  - Hostname : SPDF02PLM-GU-S 

### File
  - Name:stg01-a-tky-file-plm-gu-syst
  - InstanceType:m4.xlarge
  - InstanceID: i-0728ffa3eecfbe087
  - IP:10.184.81.203
  - USER/PASS:Administrator/eez5?XX2%X
  - Hostname : SFILE01PLM-GU-S  　

### Batch
  - Name:stg01-a-tky-batch-plm-gu-syst
  - InstanceType:t2.small
  - InstanceID: i-0edf4ef4ff3affab8
  - OS: Amazon Linux 2
  - IP:10.184.83.33
  - USER: apiadmin
  - PASS: FwtHG36a

### API
  - Name:stg01-a-tky-api-plm-gu-syst
  - InstanceType:t2.large
  - InstanceID: i-0936951be692a88dd
  - OS: Amazon Linux 2
  - IP:10.184.80.249
  - USER: apiadmin
  - PASS: A98V2r)+


### ELB

  - ELB:stg01-tky-web-plm-gu-syst
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg01-tky-web-plm-gu-syst-2053707574.ap-northeast-1.elb.amazonaws.com

  - ELB:stg02-tky-web-plm-gu-syst
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg02-tky-web-plm-gu-syst-1099709061.ap-northeast-1.elb.amazonaws.com

  - ELB:stg01-tky-api-plm-gu-syst
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg01-tky-api-plm-gu-syst-1332446110.ap-northeast-1.elb.amazonaws.com



--------------------/ Staging_Blue OperationalT/———————————————————————
  
## Staging SystemTest ( copy from GU Production) 
  
### DB1 ( Non Multi AZ )
  - DBInstanceIdentifier :stg01-tky-db-plm-gu-ope
  - Endpoint :stg01-tky-db-plm-gu-ope.chjlgx48usw9.ap-northeast-1.rds.amazonaws.com:1433
  - MasterUser/Pass:rdsmaster/Do0eAJkaYvI　　
  - InstanceType: db.r3.xlarge
  - OS: SQL Server 2014 SE
  
### DB2 ( Multi AZ )
  - DBInstanceIdentifier :stg02-tky-db-plm-gu-ope
  - Endpoint :stg02-tky-db-plm-gu-ope.chjlgx48usw9.ap-northeast-1.rds.amazonaws.com:1521
  - MasterUser/Pass:administrator/VXWwsJuMfg0　　
  - InstanceType: t2.medium
  - OS: SQL Server 2014 SE  
  
### AP1 Server
  - Name:stg01-a-tky-web-plm-gu-ope
  - InstanceType: m4.xlarge
  - InstanceID: i-0d64ddaf09667ae8a　　　
  - IP:10.184.80.119
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/2w;aYh3xPa
  - Hostname : SAP01PLM-GU-OPE 　

### AP2 Server
  - Name:stg02-c-tky-web-plm-gu-ope
  - InstanceType: m4.xlarge
  - InstanceID: i-0c32f115e655aaf22　　　
  - IP:10.184.84.35
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/(%-D?8D$;k!
  - Hostname : SAP02PLM-GU-OPE

### PDF1 Server
  - Name:stg01-a-tky-pdf-plm-gu-ope
  - InstanceType: t2.large
  - InstanceID: i-08f649ccbec28d84e　　　
  - IP:10.184.80.232
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/sCey2ReZd%
  - Hostname : SPDF01PLM-GU-O  　

### PDF2 Server
  - Name:stg02-c-tky-pdf-plm-gu-ope
  - InstanceType: t2.large
  - InstanceID: i-0ee8b18a9367ccae7　　　
  - IP:10.184.87.192
  - OS: Windows Server 2012  
  - USER/PASS:localhost\Administrator/PpA&=KCn3WZ
  - Hostname : SPDF02PLM-GU-O 

### File
  - Name:stg01-a-tky-file-plm-gu-ope
  - InstanceType:m4.xlarge
  - InstanceID: i-06780b2a680989387
  - IP:10.184.81.69
  - USER/PASS:Administrator/eez5?XX2%X
  - Hostname : SFILE01PLM-GU-O  　

### Batch
  - Name:stg01-a-tky-batch-plm-gu-ope
  - InstanceType:t2.small
  - InstanceID: i-00046dd1640b748c0
  - OS: Amazon Linux 2
  - IP:10.184.83.231
  - USER: apiadmin
  - PASS: FwtHG36a

### API
  - Name:stg01-a-tky-api-plm-gu-ope
  - InstanceType:t2.large
  - InstanceID: i-03dd5754ff7d11375
  - OS: Amazon Linux 2
  - IP:10.184.82.189
  - USER: apiadmin
  - PASS: A98V2r)+


### ELB

  - ELB:stg01-tky-web-plm-gu-ope
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg01-tky-web-plm-gu-ope-38537515.ap-northeast-1.elb.amazonaws.com

  - ELB:stg02-tky-web-plm-gu-ope
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg02-tky-web-plm-gu-ope-310764822.ap-northeast-1.elb.amazonaws.com

  - ELB:stg01-tky-api-plm-gu-ope
    - health check url: HTTP:80/iis-85.png
	-DNS name:stg01-tky-api-plm-gu-ope-1840173875.ap-northeast-1.elb.amazonaws.com


