---
title: 치트시트
description: 설명 없이 명령어만 — 실전용
tags:
  - oscp
---
DNS Enumeration

```
# IP 주소 찾기
host www.megacorpone.com

# 쿼리에 레코드 유형 지정
host -t mx megacorpone.com

# txt 명령어 반환
host -t txt megacorpone.com

```

단어 지정
`/usr/share/seclists`
- `sudo apt install seclists`

```
# 정방향 DNS 조회 자동화
cat list.txt
www
ftp
mail
owa
proxy
router

# Bash one-liner를 활용하여 호스트 이름 확인 시도
for ip in $(cat list.txt); do host $ip.megacorpone.com; done

# IP 검색
for ip in $(seq 64 79); do host 167.114.21.$ip; done | grep -Ev "not found|timed out"