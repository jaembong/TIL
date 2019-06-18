# DB가 저장될 경로 설정

```/etc/mongodb.conf``` 파일을 수정

```
# mongodb.conf

# Where to store the data.
dbpath=<원하는 경로>

#where to log
logpath=<원하는 경로>
...
```

만일 xfs로 포맷한 추가 디스크 /dev/sdb 를 이용하고 싶은 경우 일단 웒나느 디렉토리로 해당 드라이브를 마운트 후 사용 하여야 한다.

ex) /home/DB 디렉토리에 마운트할경우

```
$ mount /dev/sdb /home/DB
```

이후 ```/etc/mongodb.conf```에서 경로 수정

```
...
# Where to store the data.
dbpath=/home/DB
...
```

이후 해당 디렉토리를 ```mongodb```의 소유로 해야 정상 작동 가능

```
$ chown mongodb:mongodb -R /home/DB
```