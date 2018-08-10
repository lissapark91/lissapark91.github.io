---
layout: post
title:  "[Oracle] 컬럼 값이 null일 때 다른 값으로 .. nvl함수"
categories: query
tags: nvl, oracle, query
author: Lisa Park
description: 컬럼 값이 null일 때는 다른 값을 불러오는 nvl함수
---

## [Oracle] null 대신 다른 값을 넣어주는  nvl 함수
### 예제
Master테이블과 Detail테이블 관계가 있을 때 Detail테이블의 pk로 시퀀스를  삽입 할 때 다음과 같은 코드를 사용하였다.

    INSERT INTO LOCKER 
				( LOCKER_ZONE_ID
				  , LOCKER_NO
				  )
			VALUES ( #{lockerZoneId}
				  , nvl((select max(LOCKER_NO)+1 from LOCKER where LOCKER_ZONE_ID = #{lockerZoneId}), 0)
				   )

 기존의 시퀀스가 존재하면 max + 1을 해주고
 기존 시퀀스가 존재하지 않으면 0으로 넣어주는 nvl 함수를 구현하였다.
 

### nvl 함수
- NVL(VALUE_1 , VALUE_2)
VALUE_1이 NULL일 경우 **VALUE_2**반환, 그렇지 않을 경우 **VALUE_1**을 반환

### nvl2 함수
- NVL2(VALUE_1, VALUE_2, VALUE_3)
VALUE_1이 NULL일 경우 **VALUE_3**반환, 그렇지 않을 경우 **VALUE_2**을 반환

### decode 함수
- DECODE(VALUE, IF1, THEN1, IF2, THEN2 ..)
VALUE값이 IF1일 경우에 THEN1 값을 반환하고 VALUE 값이 IF2일 경우에 THEN2값을 반환