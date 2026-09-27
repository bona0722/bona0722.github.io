---
title: 치트시트
description:
tags:
  - oscp
---
# Information Gathering
## DNS Enumeration
호스트 발견에 사용

> [!Note]- list.txt
> www
> ftp
> mail
> owa
> proxy
> router

**DNSRecon**
DNS Enumeration 스크립트

`-d`: 도메인 이름 지정
`-t`: 열거 유형 지정 (std = standard scan, brt = brute force)
`-D`: 하위 도메인 문자열이 포함된 파일 이름 지정

- `dnsrecon -d megacorpone.com -t std`
- `dnsrecon -d megacorpone.com -D ~/list.txt -t brt`

**DNSEnum**
DNS Enumeration 자동화 도구

- `dnsenum megacorpone.com`

### Window
**nslookup**
- LIving off the Land 시나리오에서 보통 사용
- `nslookup -type=TXT info.megacorptwo.com 192.168.50.151`

window 연결
- `xfreerdp /u:student /p:lab /v:192.168.50.152`


## TCP Scanning
### CONNECT scanning
`-w`:  타임아웃을 초 단위로 지정
`-z`: zero-I/O mode 지정(데이터 전송 안 함)
- `nc -nvv -w 1 -z 192.168.50.152 3388-3390`


## UDP Scanning
`-u`: UDP Scan
- `nc -nv -u -z -w 1 192.168.50.149 120-123`
- 