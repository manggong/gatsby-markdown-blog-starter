---
date: 2019-12-20
title: "ubuntu NFS"
cover: "https://unsplash.it/400/300/?random?BoldMage"
categories:
  - Linux
tags:
  - infra
  - ubuntu
---

# Linux

## 1. NFS 서버 구현

네트워크에 연결된 컴퓨터끼리 디렉토리를 공유 할 수 있다.

### NFS 구현 순서

1. NSF 서버에 관련 패키지를 설치한다.
2. NFS 서버의 /etc/exports에 공유할 디렉터리와 접근을 허가해줄 컴퓨터, 접근 권한을 지정한다.
3. NFS 서비스를 실행한다.
4. NFS 클라이언트에 관련 패키지를 설치한다.
5. NFS 클라이언트에 showmount 명령어를 실행해 NFS 서버에 공유된 디렉터리가 있는지를 확인한다.
6. NFS 클라이언트에서 mount 명령어를 실핼해 NFS 서버에 공유된 디렉터리를 마운트한다.
