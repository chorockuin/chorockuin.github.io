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
  * zrange 'key' 'from' 'to'
  * lrange 'key' from 'to'
* Celery에서 prefetch해서 가져간 메세지들은 실제로 Celery에서 처리되기 전까지는 Redis 내 unacked_index라는 zset형태의 키로 저장된다.
* zset 속을 까보면, 요청 순서대로 번호가 매겨진 task id가 보인다.
* Celery가 순서대로 task id에 해당하는 처리를 시작하면,  zset에서 해당 task id가 제거된다.
* Celery의 prefetch 크기보다 더 많은 수의 요청이 발생하면 해당 요청들은 Redis 내 list형태의 celery라는 키로 저장된다.
* list 속을 까보면, 요청 메세지가 보인다.

## Celery
* 데몬 만들기
  * https://docs.celeryproject.org/en/latest/userguide/daemonizing.html#init-script-celeryd
* preftech는 Redis에서 미리 끌어(prefetch)와 저장해 둘 수 있는 Celery 내 최대 처리 요청 메세지의 수를 나타낸다.
* 디폴트는 4개이고,  --prefetch-multiplier 옵션으로 변경할 수 있다.
