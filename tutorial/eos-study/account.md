# 계정 생성하기

## 개요

계정을 생성하는 방법에 대하여 학습한다.

계정 생성하는 방법은 **2가지**가 있는데, `create account` 로 생성하는 방법과 `system newaccount` 로 생성하는 방법이 있다. 전자는 시스템 계정을 생성하기 위한 방식이고 후자는 메인넷환경을 구성하고 실제 이오스 환경에서 사용하는 일반 계정을 생성할 때 사용하는 방식이다. 후자는 추후에 설명한다.

## 계정 생성하기

### 1. 계정 생성 커맨드를 입력한다.

```text
cd ~/eos/build/programs/cleos
./cleos create account eosio test EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ EOS6muMvKhjH2Y5A3LgytzR8D9sTVtAreCr42f8JNYxarjX8pa3uM
```

> ```text
> Error 3120003: Locked wallet
> Ensure that your wallet is unlocked before using it!
> ```
>
> ```text
> Error 3090003: Provided keys, permissions, and delays do not satisfy declared authorizations
> Ensure that you have the related private keys inside your wallet and your wallet is unlocked.
> ```

위와 이처럼 입력하면 결괏값이 전자의 경우와 후자의 경우 둘 중 하나로 나올 것이다. 글 내용을 읽어보니 계정 생성 실패한 것처럼 보인다. 걱정하지 마시라. 학습 순서를 그대로 따라오신 분들은 이 오류 메시지가 뜰 것이다. 앞으로 자주 보게 되는 메시지이기 때문에 일부러 이 오류를 발생시켰다. 그럼 입력한 커맨드 부터 하나씩 파헤쳐 보자.

#### 첫번째 오류의 경우

지갑이 잠겨 있는 경우이다. [지갑 잠금해제 설정하기](wallet-unlock.md) 페이지에서 지갑 잠금해제 하는 방법에 대해서 학습한다.

#### 두번째 오류의 경우

일단 이 오류가 나는것은 지극히 당연한 현상이며 하나하나씩 이유를 알아보자.

`./cleos create account` : 여기까지는 단순히 계정을 생성한다는 명령어다.

`eosio` : 여기서 첫번째 인자로 사용된 eosio는 바로 모계정을 의미한다. 이오스에서는 계정을 생성하기 위해서는 반드시 계정을 생성시켜주는 모 계정이 필요하며 eosio는 처음 이오스 블록체인을 구동시킬때 단 하나만 생성되어 있는 마스터 계정이다.

`test` : 실제 생성하고자 하는 계정의 이름이다.

`EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ` : 첫번째 입력된 키는 test 계정에서 사용할 [Owner key](../../keywords/o/owner-key.md)를 지정해준다. 이때는 반드시 public key를 입력한다.

`EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ` : 두번째 입력된 키는 test 계정에서 사용할 [Active key](../../keywords/a/active-key.md)를 지정해준다. 이때는 반드시 public key를 입력한다.

계정 생성 실패 이유는 모 계정의 **private key \(Active key\)** 가 지갑안에 삽입되어 있지 않기 때문에 계정 생성을 실패 한 것이다. 일반적으로 계정을 생성하거나 토큰을 전달하거나 하는 행위는 직접 push transaction 즉, 트랜잭션을 발생시키는 행위인데, 트랜잭션을 발생시키기 위해서는 발생시키고자 하는 **1.계정**이 있어야 하고 그 계정의 **2.서명값**이 필요하며 그 계정의 서명값을 만들기 위해서는 **3.private key \( Active key\)** 가 필요하다.

쉽게 요약하자면 [`eosio`](../../keywords/e/eosio.md) 계정의 [`Active key`](../../keywords/a/active-key.md) 가 지갑안에 import를 하지 않아서 계정 생성을 실패한 것이다. 해결책은 간단하다. [`eosio`](../../keywords/e/eosio.md) 계정의 [`Active key`](../../keywords/a/active-key.md) 를 지갑안에 import 하면 된다.

### 2. EOSIO Active key import 하기

그렇다면 [`eosio`](../../keywords/e/eosio.md) 계정의 [`Active key`](../../keywords/a/active-key.md)는 어디에 있을까? [`genesis.json`](../../keywords/g/genesis.json.md) 을 직접 만들었다면, 마스터 계정의 키를 직접 지정할수 있지만 우리는 아직 학습하는 단계이기 때문에 자동생성 되어진 그대로 사용할 것이다. 추후에는 직접 [`genesis.json`](../../keywords/g/genesis.json.md) 을 생성하여 구동하는 방법을 소개할 것이다. 지금은 신경쓰지 않아도 된다.

#### eosio 계정의 key 찾기

가장 쉬운 방법으로는 eos.io 공식 홈페이지의 튜토리얼이나, [`nodeos/config.ini`](../../keywords/n/nodeos-config.ini.md) 안에서 signature-provider 에서 찾을 수 있다. 아래는 [`eosio`](../../keywords/e/eosio.md) 마스터 계정의 Active key 이다. 참고로 default로 생성된 [`eosio`](../../keywords/e/eosio.md) 계정은 [`Onwer key`](../../keywords/o/owner-key.md)와 [`Active key`](../../keywords/a/active-key.md)가 **동일**하다.

```text
5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

[`eosio`](../../keywords/e/eosio.md)의 key를 지갑에 import 하자.

```text
./cleos wallet import
```

> ```text
> private key: imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
> ```

### 3. 다시 계정 생성하기

[`eosio`](../../keywords/e/eosio.md) 계정의 키를 지갑에 삽입하였다면, 다시 한번 계정 생성하기 커맨드를 입력해보자.

```text
./cleos create account eosio test EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ EOS6muMvKhjH2Y5A3LgytzR8D9sTVtAreCr42f8JNYxarjX8pa3uM
```

> ```text
> executed transaction: c0d38a5cef42db63ec1af903d38fdac256ecf051287d3ecd016a325c8650e9a0  200 bytes  12062 us
> #         eosio <= eosio::newaccount            {"creator":"eosio","name":"test","owner":{"threshold":1,"keys":[{"key":"EOS8N1AWn6pXrKG4cyCCWYvZQU8Z...
> warning: transaction executed locally, but may not be confirmed by the network yet         ]
> ```

그럼 위와 같이 정상적으로 계정을 생성한것을 볼 수 있다.

