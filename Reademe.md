## โครงสร้าง
```bash
│   .gitignore
│   README.md
│   yarn.lock
│   setupPorts.sh
│   setup.sh
│   setPostgres.sh
│   package.json
│   package-lock.json
│   install.sh
│   docker-compose.yml
└──────data-api
        │       hv_gcp_key.pub
        │       hv_gcp_key
        │       dockerfile
        │       README.md
        │       .gitignore
        ├───────hv_data_api
        ├───────ref   
└──────decision_support_back_end
        │       yarn.lock
        │       server.js
        │       package.json
        │       package-lock.json
        │       decision.backend.router.js
        │       babel.config.js
        │       app.js
        │       Dockerfile
        ├──────config
        ├──────controllers
└──────decision_support_front_end
        │       yarn.lock
        │       README.md
        │       .gitignore
        ├───────src
        ├───────laravel-nuxt
└──────user-api
        │       user_api.router.js
        │       server.js
        │       .package.json
        │       package-lock.json
        │       README.md
        │       Dockerfile
        │       .gitignore
        │       dockerignore
        ├───────controllers
        ├───────config
└──────visit_management_back_end
        │       yarn.lock
        │       visit.backend.router.js
        │       server.js
        │       package.json
        │       package-lock.json
        │       Dockerfile
        │       .gitignore
        │       dockerignore
        │       README.md
        │       .DS_Store
        ├───────controllers
        ├───────config
└──────visvisit_management_front_end
        │       package.json
        │       package-lock.json
        │       .gitignore
        │       README.md
        │       .DS_Store
        ├───────src
        ├───────laravel-nuxt
```
# วิธีการติดตั้ง ระบบระบบสนับสนุนการทำงานของหน่วยบริการเยี่ยมบ้าน  เวอร์ชั่น 2.0

## สิ่งที่ต้องการ
### 1.1 ฮาร์ดแวร์
> 1.1.1 Ram อย่างน้อย 8 GB

> 1.1.2 Storage ขั้นต่ำ 16 GB ขึ้นไป
### 1.2 ซอฟต์แวร์
> Ubantu Version 18.04 ขึ้นไป

> Port ที่ระบบใช้คือ 3211, 3212, 4000, 3600, 3700, 3800, 3900  5050, 5432, 8081, 8082 ,9000

***หมายเหตุ** สามารถเปลี่ยน port ได้ในขั้นตอนที่ 3 ยกเว้น port 5432 ที่ไม่สามารถเปลี่ยนได้
คำสั่งเหล่านี้ให้ติดตั้งภายในเครื่อง ก่อนเป็นอันดับแรก เพื่อให้คำสั่งอื่นๆภายในโปรเจคสามารถใช้ได้
```script
$ sudo apt-get install docker
$ sudo apt-get install docker-compose
$ sudo apt-get install nodejs npm -y
$ sudo npm install -g yarn
```

## ดาวน์โหลดไฟล์และขั้นตอนการติดตั้ง
### 1.Clone โปรเจค 
 จาก https://drive.google.com/drive/folders/19azPaRgegAiDIiwoPNF1_Al_rV5fLcto
```script
https://drive.google.com/drive/folders/19azPaRgegAiDIiwoPNF1_Al_rV5fLcto
```
<p align="center">
<img src="https://media.discordapp.net/attachments/894908182734995526/926010013850415124/unknown.png">
<p align="center">ภาพที่ 1</p>
</p>


### 2. เมื่อ Clone โปรเจคมาแล้ว ข้างในจะมีไฟล์ตามภาพที่ 2
***หมายเหตุ** หลังจาก clone โปรเจคมาแล้ว ควรติดตั้งซอฟต์แวร์ที่ระบบต้องการให้เรียบร้อย
<p align="center">
<img src="https://media.discordapp.net/attachments/894908182734995526/926010131542573056/unknown.png">
<p align="center">ภาพที่ 2</p>
</p>



### 3. ถ้าต้องการเปลี่ยน port ของแต่ละ service สามารถใช้คำสั่งด้านล่าง
```script
$ ./setupPorts.sh
```
โดยใช้หมายเลข (1-7) เพื่อเลือก service ที่ต้องการเปลี่ยน port

***หมายเหตุ** หากไม่ต้องการเปลี่ยน port สามารถข้ามขั้นตอนนี้ได้ โดยระบบจะใช้ port เริ่มต้นที่ตั้งไว้
ให้แล้ว
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890238867880423504/unknown.png">
<p align="center">ภาพที่ 3</p>
</p>
ตัวอย่าง การเปลี่ยน port ของ service ชื่อ Decision suppost Front End
<br>
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890239565388984432/unknown.png">
<p align="center">ภาพที่ 4</p>
</p>



### 4. ในไฟล์ install.sh , setup.sh , setPostgres.sh , setupPorts.sh จะขึ้นเป็นสีขาว(เฉพาะครั้งแรก)
ให้ใช้คำสั่ง 
chmod 700 “ตามด้วยชื่อไฟล์” เพื่อให้สามารถใช้ 4 ไฟล์นี้ได้ในการ run
```script
$ chmod 700 setup.sh
$ chmod 700 setPostgres.sh
$ chmod 700 setupPorts.sh
```
จากนั้นไฟล์  setup.sh , setPostgres.sh , setupPorts.sh จะกลายเป็นสีเขียว

***หมายเหตุ** ถ้าไฟล์เป็นสีเขียวอยู่แล้วก็สามารถข้ามขั้นตอนนี้ได้เลย
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240105393057853/unknown.png">
<p align="center">ภาพที่ 5</p>
</p>



### 5. ทำการตั้งค่า ชื่อ โดเมน หรือ IP Address ที่ต้องการให้กับระบบ
***หมายเหตุ** ถ้าหากติดตั้งบน Local host สามารถข้ามขั้นตอนที่ 5
 โดยใช้คำสั่ง
```script
$ ./setup.sh
```
ให้ทำการกรอก โดเมน หรือ IP Address ที่ต้องการใช้

>เช่น rama-hospital.com

หลังจากนั้น กด Enter ถือว่าเสร็จเรียบร้อย
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240195025313802/unknown.png">
<p align="center">ภาพที่ 6</p>
</p>


### 6.ตั้งค่าการเข้า pgadmin เพื่อใช้ในการเข้าสู่ระบบ ในขั้นตอนที่ 8

โดยใช้คำสั่ง
```script
$ ./setPostgres.sh
```
โดยจะให้กรอก 3 อย่างคือ
> 1.กรอก username 

> 2.กรอก email 

> 3.กรอก password
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240346380972082/unknown.png">
<p align="center">ภาพที่ 7</p>
</p>

### 7. สร้างฐานข้อมูล โดยในโปรเจคนี้จะใช้ PostgresSQL 
 โดยใช้คำสั่ง
```script
$ sudo docker-compose up -d 
```
เมื่อ RUN สำเร็จให้ใช้คำสั่งด้านล่าง เพื่อตรวจสอบ service ที่กำลังทำงานอยู่
```script
$ sudo docker-compose ps
```
จะเห็นได้ว่า ณ ตอนนี้มี Service ที่กำลังทำงานอยู่คือ
> 1. pgadmin run ที่ port 5050 หรือ port ที่เปลี่ยนจากขั้นตอนที่ 3 ของ service ชื่อ pgadmin

> 2. postgres run ที่ post 5432
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240420506894426/unknown.png">
<p align="center">ภาพที่ 8</p>
</p>

### 8. เมื่อสำเร็จจะปรากฎตามภาพด้านล่าง
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241633784852500/unknown.png">
<p align="center">ภาพที่ 17</p>
</p>
### 8. ค้นหาที่อยู่ โดเมน หรือ IP Address ที่ระบุในขั้นตอนที่ 4 และตามด้วย port 5050 หรือ port ที่เปลี่ยน
จากขั้นตอนที่ 3 ของ service ชื่อ pgadmin เพื่อเข้ามาสร้าง server database ที่ใช้ภายในระบบ

ตัวอย่างเช่น 

_http://www.rama-hospital.com:5050_

จากนั้นจะเห็นหน้าปรากฏดังภาพที่ 9 ทำการ login เข้าสู่ระบบ ตามที่ระบุในขั้นตอนที่ 6

กรอก email และ password
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240480070209566/unknown.png">
<p align="center">ภาพที่ 9</p>
</p>

### 9. เมื่อเข้าสู่ระบบได้แล้ว ให้กดคำว่า **Add New Server**
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240599171670036/unknown.png">
<p align="center">ภาพที่ 10</p>
</p>
เลือก General 

ให้ใส่ Name เป็นชื่อ Server
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890240677596762182/unknown.png">
<p align="center">ภาพที่ 11</p>
</p>
เลือก Connection 

> 1. Host name/address ให้ใส่ โดเมน หรือ IP Address เช่น rama-hospital.com

> 2. ใส่ Password

> 3. ติ๊ก Save password

> 4. กด Save
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241188999856259/unknown.png">
<p align="center">ภาพที่ 12</p>
</p>

เมื่อสำเร็จจะปรากฏข้อมูลดังภาพที่ 13

หากกดดูที่ Tables จะเห็นได้ว่าตอนนี้ยังไม่มีตารางฐานข้อมูล
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241268796514335/unknown.png">
<p align="center">ภาพที่ 13</p>
</p>

### 10. เมื่อกดรีเฟรชที่ Tables จะเห็นว่ามีตารางเพิ่มเข้ามา 35 ตาราง
***หมายเหตุ** ถ้าตารางยังไม่ขึ้น ให้รอสักครู่ เพราะเนื่องจาก ขั้นตอนที่ 10 อาจยัง run ไม่เสร็จสมบูรณ์
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241427446050856/unknown.png">
<p align="center">ภาพที่ 15</p>
</p>

### 11. สร้างผู้ใช้งาน สำหรับเข้าสู่ระบบครั้งแรก
โดยให้ค้นหา ชื่อโดเมนหรือ IP Addeess ตามด้วย port 9000/user/user/ 

หรือ port ที่เปลี่ยนใหม่ในขั้นตอนที่ 3 ของ service ชื่อ Data-api-django

เช่น http://www.rama-hospital.com:9000/user/user/

จะปรากฎดังภาพ
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241749505687603/unknown.png">
<p align="center">ภาพที่ 18</p>
</p>
โดยให้กรอกตามช่อง ดังภาพด้านล่าง จากนั้นจึงกด POST
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241831357534288/unknown.png">
<p align="center">ภาพที่ 19</p>
</p>
เมื่อสำเร็จจะเป็นดังภาพที่ 20
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241898759979098/unknown.png">
<p align="center">ภาพที่ 20</p>
</p>
หากต้องการเข้าหน้า web ให้ใช้ port 8082 หรือ port ที่เปลี่ยนใหม่ในขั้นตอนที่ 3

ของ service ชื่อ Decision suppost Front End

เช่น http://www.rama-hospital.com:8082
<p align="center">
<img src="https://cdn.discordapp.com/attachments/758225208204722207/890241964618944592/unknown.png">
<p align="center">ภาพที่ 21</p>
</p>
