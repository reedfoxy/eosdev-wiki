# eosio.bios

## 개요

특수한 기능을 수행하는 [system contract](../s/system-contract.md)

[nodeos](../n/nodeos.md) 를 최초로 구동한뒤 [eosio](eosio.md) 계정으로 배포하는 [system contract](../s/system-contract.md) 이다. **자원 할당** 및 **BP를 지정**할 수 있는 기능을 가지고 있는 계약이다. 당연한 이야기지만, 일반 계정으로 배포할 경우 아무런 기능을 수행할 수 없다. 특수한 권한을 가진 [eosio](eosio.md) 계정으로 이 컨트랙트를 등록해야만 효과를 발휘할 수 있다. 참고 [eosio.system](eosio.system.md) 계약이 개발되기 이전에 **임시**로 사용했던 계약이므로 **현재는 쓰지 않는다**. 

## 파일 위치

EOS\_PATH/contracts/eosio.bios/

## 기능

1. [setpriv](eosio.bios.md#1-setpriv)
2. [setalimits](eosio.bios.md#2-setalimits)
3. [setglimits](eosio.bios.md#3-setglimits)
4. [setprods](eosio.bios.md#4-setprods)
5. [setparams](eosio.bios.md#5-setparams)
6. [reqauth](eosio.bios.md#6-requth)

### 1. setpriv

#### 개요

특정 계정에 특권을 부여하는 액션이다. 

action name은 set\_privilege를 줄여서 setpriv 라고 한다. [eosio](eosio.md) 계정은 일반 계정과 달리 [system contract](../s/system-contract.md) 를 배포하고 실행할 수 있는 권한을 가지고 있는데, 이러한 권한을 다른 계정에게 부여할 수 있는 기능이다. 만약 일반 계정에게 이 특권을 부여할경우 [eosio](eosio.md) 와 동등한 권한을 가지게 되며, [eosio](eosio.md) 계정이 사용할 수 있는 **모든 기능**을 그대로 **사용**할 수 있다. 참고로 **자기 자신**에게도 **사용**할 수 있으며 자기 자신에게 권한을 false로 줄 경우 평범한 일반 계정이 된다. 특권이 박탈 당할 경우 특권이 있는 계정이 다시 권한을 올려주지 않는다면 **되돌릴 수 있는 방법이 없으니** 주의하자.

#### 사용방법

```text
cleos push action eosio setpriv '["user1","1"]' -p eosio
```

| Parameter Type | Example | Description |
| :--- | :--- | :--- |
| account\_name | user1 | 특권을 지정 하고자 하는 계정명을 입력한다. |
| uint8\_t | 1 |  0 또는 1을 입력하면 된다. 0 = false, 1 = true |

### 2. setalimits

#### 개요

특정 계정의 [cpu](../c/cpu.md) , [net](../n/net.md) , [ram](../r/ram.md) 자원을 변경할 수 있는 액션이다. 

action name은 set\_account\_limits를 줄여서 setalimits 라고 한다. 한마디로 지정한 계정의 보유중인 자원을 마음대로 할당 및 조작할 수 있는 기능이다.

#### 사용방법

```text
cleos push action eosio setalimits '["user1","10240","1","2"]' -p eosio
```

| Parameter Type | Example | Description |
| :--- | :--- | :--- |
| account\_name | user1 | 보유자원을 변경하고자 하는 계정명을 입력한다. |
| int64\_t | 10240 | RAM 자원 \( 단위 : byte \) |
| int64\_t | 1 | NET 자원 지분 |
| int64\_t | 2 | CPU 자원 지분 |

RAM 같은 경우는 byte 단위로 설정이 가능하다. RAM 최소 보유량은 2724 이상이 되어야 한다. NET 자원과 CPU 자원은 현재 네트워크 자원의 총량과 비례하여 보유하고 있는 숫자에 따라서 비율로 배분된다. 만약 CPU와 NET를 1을 가지고 있다고 하더라도 자원을 할당받은 사람이 혼자라면 100% 전부 네트워크를 쓸 수 있다.

### 3. setglimits

#### 개요

네트워크의 전체 자원을 설정할 수 있는 액션이다.

action name은 set\_global\_limits를 줄여서 setglimits 라고 한다. 네트워크의 전체 자원 총량을 직접 설정 및 조작 할 수 있다. 그러나 코드를 열어보면 해당 액션은 정상적으로 코드 구현이 되어 있지 않으므로 현재는 **사용할 수 없다**.

### 4. setprods

#### 개요

직접 [BP](../b/bp.md) 를 지정할 수 있는 액션이다.

action name은 set\_producers 를 줄여서 setprods 라고 한다. [BP](../b/bp.md)를 직접 지정할 수 있다. 네트워크 상태에 따라서 약 몇분간 지연될 수 있다. 로컬에서 돌릴 경우 대체적으로 1분 이내에 변경된다. 최대 21명까지 지정할 수 있다.

#### 사용방법

해당 기능을 사용하기 위해서는 사전 작업이 필요하다. [EOS 학습순서](../../tutorial/eos-study/) 를 참고하여 2개 이상의 노드를 연결하고 환경설정을 수정하여야 한다. 사전 작업이 끝났다면 아래 Command를 입력한다.

```text
cleos push action eosio setprods '{"schedule":[{"producer_name":"eosio","block_signing_key":"'EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV'"},{"producer_name":"user1","block_signing_key":"'EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV'"}]}' -p eosio
```

| Parameter Type | Parameter Name | Example | Description |
| :--- | :--- | :--- | :--- |
| account\_name | producer\_name | eosio, user1 | 지정하고자 하는 BP 계정명 |
| public\_key | block\_signing\_key | 'EOS6MRyAjQq8ud...' | block 생성시 사용 할 sining key |

JSON 배열로 최대 21명까지 지정할 수 있다.

### 5. setparams

#### 개요

블록체인 환경설정 정보를 변경할 수 있는 액션이다.

action name은 set\_parameters를 줄여서 setparams라고 한다. eos 프로젝트 내부에 struct로 선언된 blockchain\_parameters 의 값을 변경할 수 있는 기능이다. 파라미터의 Description은 생략하였으며 대해 상세히 보고 싶다면 [genesis.json](../g/genesis.json.md) 을 참고하면 된다. 

#### 사용방법

```text
cleos push action eosio setparams '{"params":{"max_block_net_usage":"1048576","target_block_net_usage_pct":"1000","max_transaction_net_usage":"524288","base_per_transaction_net_usage":"12","net_usage_leeway":"500","context_free_discount_net_usage_num":"20","context_free_discount_net_usage_den":"100","max_block_cpu_usage":"100000","target_block_cpu_usage_pct":"500","max_transaction_cpu_usage":"5000","min_transaction_cpu_usage":"100","max_transaction_lifetime":"3600","deferred_trx_expiration_window":"600","max_transaction_delay":"388800","max_inline_action_size":"4096","max_inline_action_depth":"4","max_authority_depth":"6"}}' -p eosio
```

| Parameter Type | Parmeter Name | Example |
| :--- | :--- | :--- |
| uint64\_t | max\_block\_net\_usage | 1048576 |
| uint32\_t | target\_block\_net\_usage\_pct | 1000 |
| uint32\_t | max\_transaction\_net\_usage | 524288 |
| uint32\_t | base\_per\_transaction\_net\_usage | 12 |
| uint32\_t | net\_usage\_leeway | 500 |
| uint32\_t | context\_free\_discount\_net\_usage\_num | 20 |
| uint32\_t | context\_free\_discount\_net\_usage\_den | 100 |
| uint32\_t | max\_block\_cpu\_usage | 100000 |
| uint32\_t | target\_block\_cpu\_usage\_pct | 500 |
| uint32\_t | max\_transaction\_cpu\_usage | 50000 |
| uint32\_t | min\_transaction\_cpu\_usage | 100 |
| uint32\_t | max\_transaction\_lifetime | 3600 |
| uint32\_t | deferred\_trx\_expiration\_window | 600 |
| uint32\_t | max\_transaction\_delay | 3888000 |
| uint32\_t | max\_inline\_action\_size | 4096 |
| uint16\_t | max\_inline\_action\_depth | 4 |
| uint16\_t | max\_authority\_depth | 6 |

### 6. requth

#### 개요

액션을 발생시킨 계정이 본인이 맞는지 스스 검증하는 액션이다.

action name은 require\_auth 을 줄여서 requath 라고 한다. 별 특별한 기능 없는 액션이다. 본인이 발생시킨 액션이  맞는지 스스로 검증하는 코드 한줄밖에 없다.

#### 사용방법

```text
cleos push action eosio requth '["user1"]' -p user1
```

| Parameter Type | Parameter | Description |
| :--- | :--- | :--- |
| account\_name | user1 | -p user1 과 계정명이 일치하지 않으면 오류메시지가 난다. |

