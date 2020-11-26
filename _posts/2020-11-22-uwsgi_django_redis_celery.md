---
layout: post
title: "uWSGI + Django + Redis + Celery"
---
## uWSGI
* 데몬 만들기
  * https://uwsgi-docs.readthedocs.io/en/latest/Configuration.html#ini-files
  * https://uwsgi-docs.readthedocs.io/en/latest/Options.html
  * https://docs.djangoproject.com/en/3.1/howto/deployment/wsgi/uwsgi/
* 서비스 만들기
  * https://sysops.tistory.com/67
  
## Django
* 로깅
  * https://docs.djangoproject.com/en/2.2/topics/logging/
  
## Redis
* redis-cli 커맨드
  * https://redis.io/commands
  * dbsize
  * key *
  * get 'key'
  * del 'key'
  * zrange 'key' 'from index' 'to index'
  * lrange 'key' 'from index' 'to index'
  * llen 'list type key'
* broker 동작 흐름
  * worker(Celery)에 'task 수행 요청' 송신
    * celery라는 list 타입의 key에 task 정보 삽입/관리
  * worker로부터 'task 수행 요청을 수신했다'고 전달받음
    * celery key에서 task 정보 삭제
    * unacked_index라는 zset 타입의 key에 task의 uuid 삽입/관리
  * worker로부터 'task 수행 요청 ack'를 전달 받음
    * unacked_index key에서 task의 uuid 삭제
* unacked_index의 크기
  * worker가 'task 수행 요청'을 수신할 수 있는 최대 크기(Celery의 prefetch 값)
* unacked_index에 task의 uuid 값이 존재할 수 있는 시간
  * Celery 등에서 visibility_time 파라미터로 설정할 수 있음. 디폴트 1시간.
  * 존재할 수 있는 시간이 지나면, unacked_index key에서 삭제되고, celery key에 task 정보가 다시 삽입됨.
  
## Celery
* 데몬 만들기
  * https://docs.celeryproject.org/en/latest/userguide/daemonizing.html#init-script-celeryd
* 'task 수행 요청' 처리 흐름
  * 'task 수행 요청' 수신
  * 'task 수행 요청' 수락 + broker(Redis 등)에 'task 수행 요청 ack' 송신
  * task 수행
  * task 수행 완료
* task 수행 요청 ack 송신 시점은 CELERY_ACKS_LATE 옵션을 사용해 task 수행 완료 시점으로 옮길 수 있다고 하나, 실제로 되지는 않았음
* prefetch
  * preftech는 borker(Redis 등)로부터 가져올(prefetch) 수 있는 최대 task 수행 요청 수를 나타낸다.
  * 디폴트는 4개이고 --prefetch-multiplier 옵션으로 변경 가능하다.
