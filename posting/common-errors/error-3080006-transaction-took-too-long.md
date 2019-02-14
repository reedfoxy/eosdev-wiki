# Error 3080006: Transaction took too long

## 개요

트랜잭션 동작시간이 너무 오래 걸려서 생기는 오류

Error 3080006: Transaction took too long : 트랜잭션 실행 시간이 오래 걸려서 생기는 오류다. 컨트랙트 코드 복잡성이 높으면 높을수록 발생 확률이 높다.

## 해결방법

### 1. config.ini 파일을 연다.

nodeos를 동작할때 사용되는 환경설정 파일인 [config.ini](../../keywords/n/nodeos-config.ini.md) 파일을 연다.

### 2. max-transaction-time 값을 변경한다.

```text
# Limits the maximum time (in milliseconds) that is allowed a pushed transaction's code to execute before being considered invalid (eosio::producer_plugin)
max-transaction-time = 30
```

그러면 위와같이 max-transaction-time이 디폴트 값으로 30으로 설정이 되어 있다. 단위는 ms 이다. 30ms는 생각보다 매우 짧기 때문에 이 값을 넉넉한 값으로 변경하면 된다. 위 값은 CPU 성능에 따라서 차이가 많이 나기 때문에 저사양 컴퓨터를 사용하고 있다면 좀더 높게 잡아주면 된다. 그러면 정상적으로 트랜잭션 실행이 가능하다.

### 2. nodeos를 재실행 한다.

현재 동작하고 있는 nodeos를 재실행 하면 해당 옵션이 정상적으로 적용된것을 알 수 있다.

