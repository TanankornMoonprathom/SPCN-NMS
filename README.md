# SPCN-NMS
## รายชื่อสมาชิก

| ลำดับที่ | รหัสนักศึกษา      | ชื่อ-นามสกุล           | Link Github                             |
|--------| --------------- | :-----------------: | ---------------------------------------:|
| 1 | 116310400021-6 | นายธนัญกรณ์ มูลประถม   |https://github.com/TanankornMoonprathom|
| 2 | 116310400251-9 | นางสาวกาญจนา หรั่งเจริญ |https://github.com/KanchanaRangcharoen|
| 3 | 116310462005-4 | นางสาวคีตะภัทร ภิบาล    |https://github.com/keta410|
| 4 | 116310400485-3 | นายนาวิน ไชยเสนา      |https://github.com/nawinNC|
| 5 | 116310462030-2​ | นายพิสิษฐ์ กองแก้ว      |https://github.com/pphisit|


วิธีการติดตั้ง Nagios บน ubuntu วิธีการติดตั้งมีขั้นตอนดังนี้
1. ขั้นตอนในการเตรียมระบบปฏิบัติการ อัพเดต Repositories และติดตั้งแพ็คเกจที่จำเป็นและจำเป็นเพื่อใช้งาน Nagios Core.


พิมพ์คำสั่ง 
``` 
sudo apt update 
``` 
พิมพ์คำสั่ง 
```
sudo apt install autoconf gcc libc6 make wget unzip apache2 apache2-utils php libgd-dev
```
![1](https://user-images.githubusercontent.com/119097663/210220857-ef1be291-7e7e-419e-a1e7-526d567d8ea2.jpg)
![imgpsh_mobile_save](https://user-images.githubusercontent.com/119097663/210221017-95b6c702-ddd0-417a-b5d9-e204d0221c97.jpg)

2. ดาวน์โหลดซอฟต์แวร์เวอร์ชั่นปัจจุบัน


โดยพิมพ์คำสั่ง 
```
cd /tmp
```
 ![fcc117c0-d4e9-4f1b-bdb9-15968e39f2a9](https://user-images.githubusercontent.com/119097663/210221295-aa9de632-3097-4d60-a6d5-c516068d12b1.jpg)

พิมพ์คำสั่ง
```
 wget -O nagioscore.tar.gz
```
 ![091ef26d-f0c5-4197-a597-763a82883125](https://user-images.githubusercontent.com/119097663/210221472-e97ee7c2-74a6-42f8-bac8-45c634d7ceb6.jpg)

พิมพ์คำสั่ง 
```
tar xzf nagioscore.tar.gz
```
 ![image](https://user-images.githubusercontent.com/119097663/210221636-6e1e4d42-5365-46cb-957a-28f0cf501c7b.png)

3. ติดตั้งnagiosเวอร์ชั่นปัจจุบัน

พิมพ์คำสั่ง 
```
cd /tmp/nagioscore-nagios-4.4.6/
```

พิมพ์คำสั่ง 
```
sudo ./configure --with-httpd-conf=/etc/apache2/sites-enabled
```
![fcc117c0-d4e9-4f1b-bdb9-15968e39f2a9](https://user-images.githubusercontent.com/119097663/210221735-5208a6fb-5479-42ed-a7ce-a97ce38f116b.jpg)

พิมพ์คำสั่ง 
```
sudo make all
```
![265284c8-f718-4161-9524-5ab4df068867](https://user-images.githubusercontent.com/119097663/210221893-5267cec2-5712-49e1-b401-f5f6de1a4f36.jpg)

4. สร้างผู้ใช้และกลุ่ม

พิมพ์คำสั่ง 
```
sudo make install-groups-users และ sudo usermod -a -G nagios www-data
```
![68bbe1c5-a53e-4feb-9f03-351e64069f59](https://user-images.githubusercontent.com/119097663/210222021-db50df4a-8c2e-4b8b-b511-d552e80ee109.jpg)

5. ติดตั้งแพ็คเกจที่จำเป็นต่างๆ

พิมพ์คำสั่ง 
```
sudo make install
```
![9d3a9747-7823-48a5-a2c7-d4e768040e18](https://user-images.githubusercontent.com/119097663/210222147-afee7c2c-1d56-4cc5-8735-a81d37e71c89.jpg)


พิมพ์คำสั่ง 
```
sudo make install-daemoninit 
```
พิมพ์คำสั่ง 
```
sudo make install-commandmode 
```
พิมพ์คำสั่ง 
```
sudo make install-config
```

![f2000ebb-e9aa-48d9-b7df-4eea2aa5ba86](https://user-images.githubusercontent.com/119097663/210222213-504c2455-8da8-4d18-ad2a-48220df104c0.jpg)

6. ติดตั้งและกำหนดค่าไฟร์วอลล์ผ่าน IPTables

พิมพ์คำสั่ง 
```
sudo apt install iptables
```
พิมพ์คำสั่ง 
```
sudo iptables -I INPUT -p tcp --destination-port 80 -j ACCEPT
```
พิมพ์คำสั่ง sudo apt install -y iptables-persistent
![38daeabe-ec4b-4625-ba05-188ce02252b8](https://user-images.githubusercontent.com/119097663/210222466-3a45a764-524a-43cd-91e5-19258f813066.jpg)

7. สร้างบัญชีผู้ใช้ใน Apache เพื่อใช้งานใน Nagios Core


พิมพ์คำสั่ง 
```
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

8.  รีสตาร์ท และ เริ่มการใช้งาน nagios

พิมพ์คำสั่ง 
```
systemctl restart apache2.service
```
พิมพ์คำสั่ง 
```
systemctl start nagios.service
```
![4f2623bb-1c66-4ec4-9024-baeada159610](https://user-images.githubusercontent.com/119097663/210223008-4757a317-96a5-43a4-9812-6f37dda0d1cd.jpg)

9. เข้าสู่ระบบ Nagios Core 
ด้วย IP 172.31.0.214
ล็อคอินด้วย Username เเละ Password
![eb1bf9da-7dcd-41d3-9307-8fa9172bb998](https://user-images.githubusercontent.com/119097663/210223237-3db6680f-3441-42af-828b-7407bec69bf6.jpg)

เป็นอันเสร็จขั้นตอนการติดตั้ง ขั้นตอนต่อไปจะเป็นการติดตั้งปลั๊กอินหลักของ Nagios


## การติดตั้งปลั๊กอินของ Nagios มีขั้นตอนการติดตั้งดังนี้

1. อัพเดต Repositories และติดตั้งแพ็คเกจที่จำเป็นและจำเป็นเพื่อใช้งาน ปลั๊กอิน Nagios.

พิมพ์คำสั่ง 
```
sudo apt update
```
พิมพ์คำสั่ง 
```
sudo apt install autoconf gcc libc6 libmcrypt-dev make libssl-dev wget bc gawk dc build-essential snmp libnet-snmp-perl gettext
```
![6db2ec87-0646-4ffe-b703-6365e82d644a](https://user-images.githubusercontent.com/119097663/210223568-8b12aa0b-ccc9-4075-ae74-ea2745ac9492.jpg)

2. ดาวน์โหลดและเปิดใช้งาน nagios-plugins

พิมพ์คำสั่ง 
```
wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
```
![image](https://user-images.githubusercontent.com/115439255/211200494-ff38d2e8-95ea-4747-91f4-a5fde84b5a12.png)

พิมพ์คำสั่ง 
```
tar -xzvf nagios-plugins-2.3.3.tar.gz 
```
![image](https://user-images.githubusercontent.com/115439255/211200523-1331f3a5-7988-4037-b1b9-1a1c2fc9f1b6.png)


3. รวบรวมและติดตั้ง nagios-plugins
พิมพ์คำสั่ง
```
cd /nagios-plugins-2.3.3
```
พิมพ์คำสั่ง
```
./configure && make && sudo make install
```

![image](https://user-images.githubusercontent.com/115439255/211200575-434bf82a-7e2c-4cd1-bab0-b9f35d196468.png)

เสร็จสิ้นขั้นตอนการติดตั้งปลั๊กอินของ Nagios

## วิธีการเพิ่ม host
1.  แก้ไขไฟล์ hosts.cfg โดยใช้คำสั่ง
```
nano /usr/local/nagios/etc/objects/hosts.cfg 
```



2. เพิ่ม hostgroup
```
define hostgroup {
     hostgroup_name  client ; 
     alias           Client ;
}
```
3. เพิ่ม IP Address 

 ใส่ IP Address ในช่อง address 


ตัวอย่าง IP 172.31.1.17,172.31.0.81 และ 172.31.1.234


```
define host {
    use                     linux-server      ; Name of host template to use
                                              ; This host definition will inherit all variables that>
                                              ; in (or inherited by) the linux-server host template >
    host_name               Client1
    alias                   Client1
    address                 172.31.1.17
    hostgroups              client
}
define host {
    use                     linux-server      ; Name of host template to use
                                              ; This host definition will inherit all variables that>
                                              ; in (or inherited by) the linux-server host template >
    host_name               Host .0.81
    alias                   Client1
    address                 172.31.0.81
    hostgroups              client
}
define host {

    use                     linux-server       ; Name of host template to use
                                               ; This host definition will inherit all variables that>
                                               ; in (or inherited by) the linux-server host template >
    host_name               Client2
    alias                   Client2
    address                 172.31.1.234
    hostgroups              client
}
```

4. เพิ่ม service ในการทดสอบ PING,apache,SNMP
```
define service {
    use                     generic-service           ; Name of host template to use
    host_name               Client1
    service_description     check PING
    check_command           check_ping!100.0,20%!500.0,60%
    check_interval          1
    retry_interval          1
    check_period 24x7
    check_freshness 1
    contact_groups admins
    notification_interval 2
    notifications_enabled 1
}

     define service {
        use                  generic-service
        host_name            Client1
        service_description  SNMP
        check_command        check_snmp!-C public -o .1.3.6.1.4.1.2021.10.1.3.1
    }
      define service {
        use                     generic-service           ; Name of host template to use
        host_name               Client1
        service_description     check apache
        check_command           check_http
        check_interval          1
        retry_interval          1
    }

define service {
    use                     generic-service           ; Name of host template to use
    host_name               Client2
    service_description     check PING
    check_command           check_ping!100.0,20%!500.0,60%
    check_interval          1
    retry_interval          1
    check_period 24x7
    check_freshness 1
    contact_groups admins
    notification_interval 2
    notifications_enabled 1
}
     define service {
        use                  generic-service
        host_name            Client2
        service_description  SNMP
        check_command        check_snmp!-C public -o .1.3.6.1.4.1.2021.10.1.3.1
    }
      define service {
        use                     generic-service           ; Name of host template to use
        host_name               Client2
        service_description     check apache
        check_command           check_http
        check_interval          1
        retry_interval          1
    }

    define service {
    use                     generic-service           ; Name of host template to use
    host_name               Host .0.81
    service_description     check PING
    check_command           check_ping!100.0,20%!500.0,60%
    check_interval          1
    retry_interval          1
    check_period 24x7
    check_freshness 1
    contact_groups admins
    notification_interval 2
    notifications_enabled 1
}
      define service {
        use                  generic-service
        host_name            Host .0.81
        service_description  SNMP
        check_command        check_snmp!-C SPcnCPE22 -o .1.3.6.1.4.1.2021.10.1.3.1
}
```
5. restart nagios
โดยใช้คำสั่ง
``` 
systemctl restart nagios
```
6. ตรวจสอบ host ว่าสามารถใช้งานได้หรือไม่ 
โดยเข้าเว็ป
```
172.31.0.210/nagios
``` 

7. เข้าที่ Services 

![Service Status](https://user-images.githubusercontent.com/109591322/213350964-4ee42fa2-17e6-4ba3-822b-4b5c65f8148a.png)

# Service Groups
## วิธีการเพิ่ม Service Groups

1. แก้ไขไฟล์  servicegroups.cfg โดยใช้คำสั่ง
```
nano /usr/local/nagios/etc/objects/servicegroups.cfg 
``` 

2. เพิ่มชื่อ servicegroups ที่ต้องการ เช่น snmp
```
define servicegroup {
    servicegroup_name  snmp
    alias              snmp services
}
```
3. บันทึก

4. แก้ไขไฟล์ hosts.cfg โดยใช้คำสั่ง
```
nano /usr/local/nagios/etc/objects/hosts.cfg 
```

5. เพิ่มคำสั่งด้านล่างที่ define service ของ SNMP
```
servicegroups snmp
```

ตัวอย่าง 

```
define service {
        use                  generic-service
        host_name            Host .0.81
        service_description  SNMP
        check_command    check_snmp!-C SPcnCPE22 -o .1.3.6.1.4.1.2021.10.1.3.1
        servicegroups snmp
}
```
6. บันทึก และ restart nagios
โดยใช้คำสั่ง
``` 
systemctl restart nagios
```

7. ตรวจสอบที่
```
172.31.0.210/nagios
``` 

8. เข้าที่ servicegroups เพิ่มตรวจสอบว่าได้เพิ่มถูกต้องหรือไม่


![Service Status](https://user-images.githubusercontent.com/109591322/213353760-023c7cf3-365d-46e6-baba-f8380984ee34.png)

# Client
## การติดตั้งใน Client ประกอบไปด้วย 
* snmp, snmpd
มีขั้นตอนในการติดตั้ง ตามลำดับ ดังนี้
1. อัพเดท ubuntu และเริ่มติดตั้ง SNMP, SNMPD  
```
$ apt-get update
$ apt-get install snmp snmpd libsnmp-dev 
``` 
2. เข้า file เพื่อกำหนด **agentAddress** และกำหนดการมองเห็นของ **Community** มีขั้นตอนการทำงาน ดังนี้
    
    2.1 เข้า file **snmpd.conf**
    ```
    $ sudo nano /etc/snmp/snmpd.conf
    ``` 
    2.2 แก้ไขไฟล์ snmpd.conf 

    * กำหนด **agentAddress**

        _ตัวอย่างการแก้ไข_
        ```
        agentAddress 172.31.1.206,[::1]
        //agentAddress IP-Client
        ``` 

    * กำหนดการมองเห็น **Community**

        _ตัวอย่างการแก้ไข_
        ```
        #Views
        #arguments viewname included [oid]
        #system + hrSystem groups only
        view   systemonly  included   .1.3.6.1.2.1.1
        view   systemonly  included   .1.3.6.1.2.1.25.1
        //เพิ่มการมองเห็นของ Community SPcnCPE22//
        view   systemonly  included   .1.3.6.1.4.1.2021.10.1.3.1  
        ```
        จากนั้นบันทึก file ด้วยคำสั่ง ``` ^X ``` และยืนยันการบันทึก ``` Y ``` ตามลำดับ
3. restart และ check status การทำงานของ snmpd ตามลำดับ
    ```
    $ systemctl restart snmpd 
    $ systemcrl status snmpd
    ```
_ตัวอย่าง หน้าจอผลลัพธ์การทำงานของ systemctl restart และ status snmpd_

> ผลลัพธ์ restart และ status snmpd
    ![restart-status-snmpd](https://user-images.githubusercontent.com/104758471/211152302-8aac16d7-5262-490e-bf80-27c2aafe2ef2.png)

## การอ่านผลของเครื่องมือ
สามารถดูภาพรวมของHost StatusและService Status ผ่านหน้า Services 
![Service Status](https://user-images.githubusercontent.com/109591322/213350964-4ee42fa2-17e6-4ba3-822b-4b5c65f8148a.png)

สามารถดูภาพรวมของHost StatusและService Status ผ่านหน้า Services

![สกรีนช็อต_25660107_150510](https://user-images.githubusercontent.com/119097660/211141861-dfadbd2c-ba24-4be3-ad46-f2bffb1b811c.png)

โดยผลของHost Status จะมีอยู่ 4 ค่า

![สกรีนช็อต_25660107_154000](https://user-images.githubusercontent.com/119097660/211141904-c2970cbd-17bf-411a-8bb1-824fccf87fe1.png)

  - Up
    - Up จะเป็นค่าที่บอกว่า Hostของเรานั้นตรวจสอบสำเร็จและกำลังทำงานอยู่
  - Down
    - Down จะเป็นค่าที่บอกว่า Hostของเรานั้นไม่ทำงาน
  - Unreachable	
    - Unreachable จะเป็นค่าที่บอกว่า Hostของเรานั้นไม่สามารถเข้าถึงได้
  - Pending
    - Pending จะเป็นค่าที่บอกว่า Host กำลังรอตรวจสอบ
    
ผลของService Status จะมีอยู่ 5 ค่า

![สกรีนช็อต_25660107_154006](https://user-images.githubusercontent.com/119097660/211141905-df434023-830b-4212-a6db-7f0558770281.png)
  
  - Ok
    - Ok จะเป็นค่าที่บอกว่า Service กำลังทำงานอยู่
  - Warning
    - Warning จะมีค่าเท่า Down ซึ่งบอกว่า Service นั้้น Down อยู่
  - Unknown	
    - Unknown จะเป็นค่าที่บอกว่า config ค่าผิด ให้ทำการconfigใหม่ 
  - Critical
    - Critical จะมีค่าเท่า Unreachable บอกว่า Service นั้้นไม่สามารถเข้าถึงได้
  - Pending
    - Pending จะเป็นค่าที่บอกว่า Service กำลังรอตรวจสอบ
    
Host GroupsและService Groups จะเป็นการแบ่งแยกกลุ่มเเพื่อให้ดูได้ง่าย
![สกรีนช็อต_25660107_211843](https://user-images.githubusercontent.com/119097660/211155766-b8c29cd5-11aa-4422-88df-e162cf19e5aa.png)

หน้า Map จะเป็นหน้าที่แสดงแผนภาพ Host
![สกรีนช็อต_25660107_211824](https://user-images.githubusercontent.com/119097660/211155947-4603b8e7-465c-42e9-bee3-21e3683e95b4.png)

หน้า Alerts จะแสดงประวัติแจ้งเตือนโฮสต์และบริการทั้งหมด
![สกรีนช็อต_25660107_211859](https://user-images.githubusercontent.com/119097660/211155815-fe2c1aef-ba1b-4af1-a7a5-0917c71ba94d.png)

หน้าNotifications จะแสดงการแจ้งเตือนผู้ติดต่อทั้งหมด
![สกรีนช็อต_25660107_143253](https://user-images.githubusercontent.com/119097660/211155959-b88e2f3c-dabc-4545-8cb3-bbe7f32d491c.png)

