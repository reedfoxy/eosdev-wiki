# 지갑 잠금해제 설정하기

## 개요

지갑 잠금하는 방법과 잠금해제 하는방법, 그리고 자동장금 시간을 설정하는 방법에 대해서 학습한다.

키를 저장하고 있는 지갑은 매우 중요하다. 그 이유는 private key 리스트가 저장되어 있는 중요한 파일이기 때문이다. 그래서 지갑은 잠금기능이 내장되어 있는데 이 잠금 기능을 어떻게 사용하는지 알아보자.

## 1. 지갑 잠금하기

기존에 생성해 놓았던 Default 지갑을 잠금해 보자. 아래와 같이 커맨드를 입력한다.

```text
./cleos wallet lock
```

> ```text
> Locked: default
> ```

정상적으로 잠금 처리가 되었다. 지갑을 잠금처리하게 된다면 추후 학습을 진행하겠지만 트랜잭션을 발생시킬때 지갑을 unlock 하라는 메세지가 표시되면서 사용할 수 없다. 

{% hint style="info" %}
만약 testkeys 라는 지갑을 잠금하고 싶다면 ./cleos wallet lock -n testkeys 으 사용하면 된다.
{% endhint %}

## 2. 지갑 잠금해제

```text
./cleos wallet unlock
```

> ```text
> password:
> ```

비밀번호를 입력화면이 나온다. 이때 입력해야 되는 비밀번호는 [지갑 만들기](wallet-create.md) 편에서 지갑 생성시 표시되는 지갑 비밀번호이다. 만약 이 지갑 비밀번호를 잊어버렸을 경우 해당 지갑은 더이상 사용할 수 있는 방법이 없으므로 포기하는것이 좋다. 지갑을 생성할때 콘솔창에 표시된 **비밀번호를** 입력한다면  

> ```text
> password: Unlocked: default
> ```

지갑이 정상적으로 Unlock 된것을 볼 수 있다.

## 3. 지갑 자동잠금 시간 설정하기

트랜잭션을 **15분**동안 발생시키지 않으면 지갑은 자동 Locked 처리가 된다. 보안을 위해서는 좋은 방법이지만 이오스를 테스트용으로 쓰기에는 잠금해제 하는것은 매우 귀찮은 행위가 아닐 수 없다. 환경설정을 통해 잠금해제 시간을 설정해 보도록 하자.

```text
vim ~/eosio-wallet/config.ini
```

본인이 원하는 편집기로 config.ini 파일을 열어보자.

```text
# Timeout for unlocked wallet in seconds (default 900 (15 minutes)). Wallets will automatically lock after specified number of seconds of inactivity. Activity is defined as any wallet command e.g. list-wallets. (eosio::wallet_plugin)
unlock-timeout = 900
```

파일 내용중 unlock-timout 이라는 부분이 있는데 디폴트로 900으로 설정되어 있다. 초 단위 이기 때문에 본인이 마음대로 수정하여 저장하면 된다. 저장 후에는 keosd 를 재 구동 하여야 적용이 완료된다.

