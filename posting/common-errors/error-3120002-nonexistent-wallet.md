# Error 3120002: Nonexistent wallet

## 개요

내가 생성한 지갑을 찾지 못하는경우 발생하는 오류

Error 3120002: Nonexistent wallet Are you sure you typed the wallet name correctly?

## 해결방법

### 1. 실제 wallet 파일이 존재하는지 확인한다.

```text
cd ~/eosio-wallet/
ls
```

> ```text
> config.ini     default.wallet keosd.sock     wallet.lock     test.wallet
> ```

내가 찾고자 하는 지갑 이름이 `test` 이라고 할때, 실제 지갑파일이 존재하는지 확인한다. 위와 같은 경우 test.wallet 파일이 존재하는것을 확인할 수 있다.

### 2. 원하는 wallet 파일을 open 한다.

```text
cleos wallet open -n test
```

지갑파일을 오픈 한다.

### 3. 지갑이 정상적으로 오픈 되었는지 확인한다.

```text
cleos wallet list
```

> ```text
> Wallets:
> [
>   "default",
>   "test",
> ]
> ```

정상적으로 open 된 것을 확인할 수 있다.

### 4. 지갑을 unlock 한다.

```text
cleos wallet unlock -n test
```

이제 지갑을 찾지 못한다는 오류가 표시되지 않을 것이다.

지갑 자동잠금 시간을 조절하고 싶다면 [지갑 잠금해제 설정하기](../../tutorial/eos-study/wallet-unlock.md) 페이지를 참고하면 된다.

