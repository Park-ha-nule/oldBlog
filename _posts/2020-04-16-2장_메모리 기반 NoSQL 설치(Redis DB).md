---
layout: post
title:  NoSQL
date:   2020-04-15 22:59:00 +0000
description: 메모리 기반 NoSQL 설치(Redis DB)
img: NoSQL.png
tags: [More]
author: begginer_
---

# 2장_메모리 기반 NoSQL 설치(Redis DB)

---

- 설치 환경
    - Cent OS 7 minimal
    - Java 1.8
    - Redis 5.xx
- 설치 방법
    - 자바처럼 tar로 압축된 파일 기반 설치

        -Redis 제작사에서 제공하는 방법

        -Redis DB 실행할 때마다 기본 설정을 재정의해야 함

    - Yum을 이용한 설치
- Yum을 통한 Redis 설치
    - Yum Repository는 Redis에 대한 정보가 없어 기본 Yum으로 설치 불가
    - 확장된 Repository를 설치해야함
    - EPEL(Extra Packages for Enterprise Linux) Repository 설치

        (vmware에서 cent OS를 킨 후)yum install epel-release

    - Redis 설치

        yum install redis

    - yum을 통한 redis 설치 여부 확인

        yum list installed redis

    - Redis 실행 및 실행여부 확인

        systemctl start redis

        systemctl status redis

    - Cent Os 재부팅시, Redis DB 자동실행

        systemctl enable redis

- Redis 실행 테스트
    - 네트워크 살아있는지 테스트 명령어 실행

        redis-cli : Redis 클라이언트 데몬 사용

        ping

        - Key : foo
        - Value : hi~~
        - set(저장하기)foo(중복되지 않는 key 값)hi~~(저장되는 값)
        - get(가져오기)foo(중복되지 않는 key 값)
- Redis 설정파일
    - /etc/redis.conf
    - 외부 접속 허용 설정
    - DB 패스워드 설정
    - 보호모드 해제(웬만해선 하지않는 것을 권장)