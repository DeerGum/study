# AWS Timezone 변경

명령어
```bash
$ date
Tue Jan 25 10:04:19 UTC 2022
$ sudo date
Tue Jan 25 10:04:35 UTC 2022
$ sudo cat /etc/localtime
TZif2UTCTZif2UTC
UTC0
$ sudo rm /etc/localtime
$ sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
$ date
Tue Jan 25 19:05:20 KST 2022
```

