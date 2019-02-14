# Error 3040011: The transaction can not be found

## Error 3040011

### 개요

트랜잭션 정보를 조회하려 하나 트랜잭션을 찾을 수 없는 경우. 트랜잭션id는 유효하나 block number를 힌트로 제공해야만 하는 경우.

문제 예시\)

```text
$ cleos get transaction 1d0a725873dc2257ff5f39176e388a18a95680d4102f0357757c2c75a4ed337e
Error 3040011: The transaction can not be found
Error Details:
Transaction 1d0a725873dc2257ff5f39176e388a18a95680d4102f0357757c2c75a4ed337e not found in history and no block hint was given
```

### 해결방법

트랜잭션id로 트랜잭션 정보를 조회할 때 block number를 힌트로 제공하지 않으면 위와 같은 에러가 발생할 수 있다. 만일 block number를 힌트로 제공하지 않더라도 트랜잭션 정보를 조회하고 싶다면 노드에 아래와 같은 설정을 해주어야 한다.

1\) 노드에 eosio::history\_plugin을 추가한다.

2\) config.ini에 `filter-on = *` 옵션을 추가한다.

3\) hard-replay로 노드를 재실행한다.

이렇게 하면 block number를 힌트로 제공하지 않아도 트랜잭션 정보를 조회할 수 있답니다.

### 주의할점

위 방법은 모든 트랜잭션 정보를 history에 기록하게 되기 때문에 데이터 용량을 많이 소모할 수 있는 단점이 있습니다.

