---
title: 치트시트
description: 설명 없이 명령어만 — 실전용
tags:
  - oscp
---

> [!tip]
> 설명은 각 기법 노트에. 여기는 손이 기억하기 전까지 보는 곳입니다.

## 정찰

```bash
# 전체 포트 빠르게
nmap -p- --min-rate 10000 -T4 $IP -oN ports.txt

# 열린 포트만 상세
nmap -p 22,80,445 -sCV $IP -oN detail.txt

# UDP 상위 100
sudo nmap -sU --top-ports 100 $IP
```

## 웹

```bash
# 디렉터리
gobuster dir -u http://$IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html

# 서브도메인
ffuf -u http://$IP -H "Host: FUZZ.target.com" -w subdomains.txt -fs 1234
```

## SMB

```bash
enum4linux -a $IP
smbclient -L //$IP -N
smbmap -H $IP
```

## 리버스 셸

```bash
# 리스너
nc -lvnp 4444

# 셸 업그레이드
python3 -c 'import pty;pty.spawn("/bin/bash")'
# Ctrl+Z → stty raw -echo; fg → Enter ×2
export TERM=xterm
```

## 권한 상승

```bash
# Linux
sudo -l
find / -perm -4000 -type f 2>/dev/null
cat /etc/crontab

# Windows
whoami /priv
systeminfo
```

## 파일 전송

```bash
# 공격자
python3 -m http.server
