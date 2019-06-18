# 디스크 XFS 포맷 및 마운트

### 디스크 확인

```bash
fdisk -l
```

OS 가 설치 되지 않은 추가 하드 디스크 /dev/sdb를 XFS로 포맷

```bash
mkfs.xfs -f /dev/sdb
```

이후 ```/etc/fstab``` 최하단에 다음을 추가

```
/dev/sdb <마운트할 디렉토리> xfs defaults 0 0
```

참고:

https://www.manualfactory.net/10607
