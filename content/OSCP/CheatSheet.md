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


## Netcat
**CONNECT scanning**
`-w`:  타임아웃을 초 단위로 지정
`-z`: zero-I/O mode 지정(데이터 전송 안 함)
- `nc -nv -w 1 -z 192.168.50.152 3388-3390`

**UDP Scanning**
`-u`: UDP Scan
- `nc -nv -u -z -w 1 192.168.50.149 120-123`


## Nmap
**Scan 유형**
`-sS`: TCP SYN scan (root일 때 기본값, 핸드셰이크 미완료로 빠르고 로그 적음)
`-sT`: TCP connect scan (root 없거나 proxychains 경유 시)
`-sU`: UDP scan (SNMP 161, TFTP 69 등)
`-sn`: 포트 스캔 없이 호스트 발견만 (ping sweep)

**포트 지정**
`-p <ports>`: 포트 지정 (`-p 22,80,445`, `-p 1-1000`)
`-p-`: 전체 포트 (1-65535)
`--top-ports <n>`: 흔한 포트 n개 (UDP 스캔 시간 절약용)

**서비스 / OS / 스크립트**
`-sC`: 기본 스크립트 실행
`-sV`: 서비스 버전 탐지
`-O`: OS 탐지
`-A`: `-sC -sV -O --traceroute` 묶음
`--script <name>`: 특정 스크립트 실행 (`vuln`, `smb-*`, `http-enum`)

**호스트 발견 / 속도**
`-Pn`: Ping scan 비활성화 (ICMP 차단 환경에서 거의 항상 사용)
`-n`: DNS 역질의 생략
`-T4`: 빠른 타이밍
`--min-rate 1000`: 초당 최소 패킷 수 보장 (전체 포트 스캔 단축)

**출력**
`--open`: 열린 포트만 출력
`-v`: 진행 상황 표시
`-oN <file>`: 텍스트 저장
`-oA <name>`: txt, xml, grep 형식 한 번에 저장

**자주 쓰는 조합**
- 전체 포트 빠르게 발견: `nmap -p- --min-rate 1000 -T4 -Pn -n --open -oA full 192.168.50.149`
- 발견된 포트만 상세 스캔: `nmap -p 22,80,445 -sC -sV -oA detail 192.168.50.149`
- UDP: `sudo nmap -sU --top-ports 20 -oA udp 192.168.50.149`
- 살아있는 호스트 찾기: `nmap -sn 192.168.50.0/24`

 
 SMB
 - `nmap -v -p 139,445 -oG smb.txt 192.168.50.1-254`
 - 