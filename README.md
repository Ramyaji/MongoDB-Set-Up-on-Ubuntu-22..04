# MongoDB-Set-Up-on-Ubuntu-22.04
Install and Set up MongoDB on Ubuntu 22.04 EC2


Document referred from
https://medium.com/@namestarlit/mongodb-installation-on-ubuntu-22-04-lts-6399803c1169
https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
https://www.mongodb.com/try/download/community
https://www.mongodb.com/docs/compass/current/install/
https://docs.google.com/document/d/1smYmCNT_EhqbLi2zxBisZYYDIxQlJvUgrMdFlzOqMys/edit?pli=1




*Launch EC2 Ubuntu 22.04
security group: tcp 27017 0.0.0.0/0


Commands used
1  sudo apt update
    2  apt-get upgrade
    3  sudo apt install mongodb
    4  cat /etc/lsb-release
    5  sudo apt-get install gnupg curl
    6  curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc |    sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg    --dearmor
    7  echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
    8  sudo apt-get update
    9  sudo apt-get install -y mongodb-org
    
   10  echo "mongodb-org hold" | sudo dpkg --set-selections
   11  echo "mongodb-org-database hold" | sudo dpkg --set-selections
   12  echo "mongodb-org-server hold" | sudo dpkg --set-selections
   13  echo "mongodb-mongosh hold" | sudo dpkg --set-selections
   14  echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
   15  echo "mongodb-org-tools hold" | sudo dpkg --set-selections
   
   16  sudo systemctl start mongod
   17  sudo systemctl daemon-reload
   18  sudo systemctl status mongod
   19  sudo systemctl status mongod.service
   
   20  sudo vim /etc/mongod.conf
   
   SET MONGO TO ACCESS GLOBALLY
   NEED TO CHANGE IN /etc/mongod.conf
    sudo vim /etc/mongod.conf
    net:
    port: 27017
    bindIp: 0.0.0.0 
   
   21  mongosh
   22  sudo systemctl enable mongod
   23  sudo systemctl restart mongod
   24  mongosh

   after execution of above commands now lets connect to MongoDB using MongoDB Compass from Local OS


   useful Notes
   https://drive.google.com/file/d/1-x3B4r9ijsoITqXsgHjp2CKKuupJBASS/view

   Create Database using CLI
   mongosh
   show dbs
   use PKR_MongoDB

   db.createUser({
    user: "Accelya_Dev",
    pwd: "Purple@$123",
    roles: [{ role: "readWrite", db: "PKR_MongoDB" }]
})



######
db.createUser({
    user: "developer",
    pwd: "password123",
    roles: [{ role: "readWrite", db: "my_database" }]
})
######

connection string to connect mongodb for developer

mongodb://Accelya_Dev:Purple@$123@54.210.129.158:27017/PKR_MongoDB

###### READ ACCESS #####

db.createUser(
            {
                user: "Junior_1",
                pwd: "read@access1",
                roles: [ { role: "read", db: "PKR_MongoDB" } ]
            }
        )

###### READ AND WRITE ACCESS #####

        db.createUser(
            {
                user: "Senior_1",
                pwd: "readwrite@access1",
                roles: [ { role: "readWrite", db: "PKR_MongoDB" } ]
            }
        )


#### HOW JUNIOR ACCESS DB WITH READ PERMISSION THE CONNECTION URI ####
mongodb://Junior_1:read@access1@54.210.129.158:27017/PKR_MongoDB?authSource=PKR_MongoDB

OR DNS instead IP is better security
mongodb://Junior_1:read@access1@ip-172-31-28-226.ec2.internal:27017/PKR_MongoDB?authSource=PKR_MongoDB




#### HOW SENIOR ACCESS DB WITH READ&WRITE PERMISSION THE CONNECTION URI ####
mongodb://Senior_1:readwrite@access1@54.210.129.158:27017/PKR_MongoDB?authSource=PKR_MongoDB

OR  

mongodb://Senior_1:readwrite@access1@ip-172-31-28-226.ec2.internal:27017/PKR_MongoDB?authSource=PKR_MongoDB




Create Database using CLI
   mongosh
   show dbs
   use tkp_Dev_DB

    db.createUser({
    user: "tkp_Dev_User",
    pwd: "P6V-WM}NY@DcxQ",
    roles: [{ role: "readWrite", db: "tkp_Dev_DB" }]
})


--------------------------------------------------------------------

db.createUser(
            {
                user: "tkp_Dev_User",
                pwd: "P6V-WM}NY@DcxQ",
                roles: [ { role: "readWrite", db: "tkp_Dev_DB" } ]
            }
        )

------------------------------------------------------------------------
mongodb://tkp_Dev_User:P6V-WM}NY@DcxQ@host_dns:27017/tkp_Dev_DB?authSource=tkp_Dev_DB







db.createUser(
            {
                user: "tkp_stg_User",
                pwd: "ZRx9-Dsr3:TgKw",
                roles: [ { role: "readWrite", db: "tkp_stg_DB" } ]
            }
        )

show dbs
   use tkp_stg_DB

   db.createUser({
    user: "tkp_stg_User",
    pwd: "ZRx9-Dsr3:TgKw",
    roles: [{ role: "readWrite", db: "tkp_stg_DB" }]
})
-----------------------------------------------------------------------------------------------------------

mongodb://tkp_stg_User:ZRx9-Dsr3%3ATgKw@ehost_dns:27017/tkp_stg_DB?authSource=tkp_stg_DB




   
