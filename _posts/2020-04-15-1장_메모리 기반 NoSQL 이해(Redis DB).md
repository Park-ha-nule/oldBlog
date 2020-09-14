---
layout: post
title:  NoSQL
date:   2020-04-15 22:59:00 +0000
description: 메모리 기반 NoSQL 이해
img: NoSQL.png
tags: [More]
author: begginer_
---

# 1장_메모리 기반 NoSQL 이해(Redis DB)

---

- 메모리 기반 NoSQL이란?
    - 방대한 양의 데이터 처리함에 있어 처리 속도가 느린 RDBMS의 문제점을 해결하기 위해 NoSQL 기술이 등장함
    - NoSQL 기술 적용된 DB

        -MongoDB, Cassandra DB, Hbase 등

    - 짧은 시간 안에 급격하게 증가되는 데이터 처리에 있어 기존 NoSQL 방식도 처리속도의 한계가 발생함
    - 이에 대한 대응 방법으로 메모리에 데이터를 저장하는 NoSQL 기술이 개발된

        -대표적인 기술은 Redis DB

- Redis 특징
    - 인-메모리(In-Memory) 기술

        -일반적으로 메모리를 활용한 기술들을 인-메모리 기술이라 부름

    - 오픈 소스로 배포됨(무료)
    - 저장 장소는 메모리

        -기존 NoSQL과 달리 하드디스크(HDD, SSD)가 아닌 메모리(Ram)에 저장

    - Redis는 메모리에 저장되기 때문에 메모리 관리가 중요

        -Physical Memory(Ram) 이상을 사용하면 문제가 발생

        -일반적으로 32Gb 램은 24Gb까지만 데이터 저장 공간으로 사용 권장

    - 한정된 메모리 용량 이상으로 데이터 저장이 필요할 때 해결방안은?(예를들어, 메모리(램)이 32인데 40을 저장하고 싶다면?)

        -답.SWAP 사용

        -리눅스는 가상메모리를 SWAP으로 정의하며, 부족한 메모리의 용량을 하드디스크(HDD, SSD)로부터 용량으로 끌어와서 사용함

        -40Gb 데이터 저장의 경우, 메모리(Ram) : 32Gb + 하드디스크 : 8Gb

        -단, SWAP에 저장된 데이터는 메모리가 아닌 하드디스크에 저장되기 때문에 데이터 처리(읽기, 연산) 속도가 하드디스크 속도로 처리함

        -즉, SWAP에 저장된 데이터는 속도가 많이 느림

        -결론

        -임시 방편으로 SWAP을 활용해서 장애를 대처할 순 있지만, 메모리 용량보다 큰 데이터 저장은 하지 않는 것을 권장함

- Redis 데이터 저장 구조
    - 다양한 데이터 구조를 저장할 수 있음

        -String, set, sorted-set, hashes, list

        -Hyperloglog, bitmap, geospatial index

        -Stream

    - 저장되는 데이터 구조는 한가지만 선택가능

        -어떤 데이터는 String, 어떤 데이터는 list와 같이 여러가지 데이터 구조 저장 불가

        -초기 DB 설계할 때 명확히 정의해야 함

    - **메모리 저장 크기 줄이는 것이 중요하기 때문에 Ziplist 인코딩이 되는 구조를 사용하는 것을 권장**

       <center><img src="/assets/img/NoSQL/01.png"></center>

    - 기본적으로 Collection 데이터 구조의 다양한 자료 구조를 융합해서 생성됨

        -Hash → HashTable을 하나 더 사용

        -Sorted Set → Skiplist와 HashTable을 사용

        -Set → HashTable 사용

    - 위의 **Collection 데이터 구조들은 메모리를 많이 사용**함
- Redis 데이터 처리 방법?
    - Redis Db는 싱글 쓰레드(Single Threaded)로 데이터 처리를 수햄
    - 즉, 하나의 명령이 실행되면, 그 명령이 끝날때까지 다른 명령은 실행되지 않고 대기
    - 만약, 처리 시간이 오래 걸리는 명령어를 실행하면? → 망한다.
- 처리 시간이 긴 명령의 예
    - KEYS

        -저장된 데이터의 키 값을 모두 불러오는 명령

    - FLUSHALL, FLUSHDB

        -Redis DB에 전체 데이터베이스 정보 넣어주는 명령

    - Delete Collections

        -여러 개의 컬렉션을 삭제하는 명령

    - Get All Collections

        -전체 컬렉션 정보를 가져오는 명령

- 전체 컬렉션 데이터를 가져와야 하는 경우는?
    - 전체 가져오는 프로그램 만들면 안됨
    - 데이터 저장할 때, 여러 개의 Collection으로 목적에 따라 구분하여 저장

        -Collection마다 약 5천개 레코드 이하로 저장하도록 설계 권장

- Redis DB 적용 사례
    - 캐시 서버로 활용

        -네이버, 카카오 등 사용자 수가 많은 웹 서비스에서 모두 적용되어 운영되고 있음

- Redis DB 잘못 적용된 예
    - 회원 로그인 기능 구현을 위해 Oauth 사용

        -기존 전통적인 시스템은 웹 서버의 Session을 통해 로그인 처리를 수행함

        -Session은 웹 서버의 메모리에 저장되는 구조로 한번 로그인한 사용자는 그 웹 서버에서만 로그인 여부 판단 가능함

        -사용자가 많은 경우, 여러 대의 서버로 서비스를 제공하기 때문에 세션으로 로그인 처리 불가능

        -이에 대한 해결 방안으로 Oauth 기능이 나옴

        -Oauth는 보안적으로 아주 좋은 거라고 생각하면 됨(Session은 내 컴퓨터에서 로그인이 가능하다고 생각하면 되는데, 내 컴퓨터 서버가 로그인이 안되는 경우, Oauth의 경우에서는 구글이나 카카오로 로그인이 가능함) 그래서 보안적으로 아주 괜찮음

    - Spring security oauth RedisTokenStore 이슈

        -사용자가 적은 서비스는 문제 없이 동작 가능

        -단 ,사용자 계정이 100만명이 넘게 로그인한 경우, 처리속도의 급격한 하락으로 서비스 장애 발생