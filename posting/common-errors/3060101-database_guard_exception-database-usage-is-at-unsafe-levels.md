# 3060101 database\_guard\_exception: Database usage is at unsafe levels

## 개요

chain-state-db-size-mb 사이즈가 위험 도달에 도달하였기에 나타나는 오류

[nodeos/config.ini](../../keywords/n/nodeos-config.ini.md) 에 chain-state-db-size-mb 값이 설정되어 있다. 만약 설정된 값을 초과할 경우 nodeos 구동이 멈추며 오류가 발생하게 된다. 가드 용량이 설정되어 있기 때문에 크게 걱정은 하지 않아도 된다.

## 오류 메세지

> Failed to start a pending block, will try again later
>
> 3060101 database\_guard\_exception: Database usage is at unsafe levels
>
> Database has reached an unsafe level of usage, shutting down to avoid corrupting the database. Please increase the value set for "chain-state-db-size-mb" and restart the process!
>
> Details: 3060101 database\_guard\_exception: Database usage is at unsafe levels

## 해결방법

### 1. config.ini 파일을 연다.

[nodeos/config.ini](../../keywords/n/nodeos-config.ini.md) 파일을 연다.

### 2. chain-state-db-size-mb 용량을 변경한다.

```text
# Maximum size (in MiB) of the chain state database (eosio::chain_plugin)
chain-state-db-size-mb = 1024
```

기본값으로 1024가 설정되어 있다. 이 값을 적절한 값으로 변경한다. 단위는 MB 이다. 만약 물리적인 램 보다 높게 잡을 경우 추후 심각한 속도 저하가 발생할 수 있으니 주의



