# 몽고디비 액세스 컨트롤

몽고 디비 사용시 액세스 컨트롤설정 하지 않을시 Warning문구를 띄운다.

```
2019-06-18T15:00:39.234+0900 I CONTROL  [initandlisten] 
2019-06-18T15:00:39.234+0900 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2019-06-18T15:00:39.234+0900 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2019-06-18T15:00:39.234+0900 I CONTROL  [initandlisten] 
```

### 계정 생성

```mongo``` 실행후

```
> use admin
switched to db admin
> db.createUser({user: <원하는 계정명>, pwd: <원하는 PW>, roles:["root"]})
Successfully added user: { "user" : "dbAdmin", "roles" : [ "root" ] }
```

이후 ```/etc/mongodb.conf``` 파일에서 ```auth = true``` 추가하거나 앞의 주석을 치운다.

```service mongodb restart```로 몽고디비 재시작하면 auth모드 활성화됨

이후 

```
$ mongo -u <id> -p <pw> --authenticationDatabase "admin"
```

으로 몽고디비 쉘에 재진입후 사용할 ```use <DB명>``` 으로 DB 생성후 해당 DB에서

```
db.createUser({user: <id> , pwd: <pw> , roles:["dbOwner"]})
```

로 해당 DB의 소유자 계정을 생성할수 있다.
