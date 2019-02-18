# Error 3090003: Provided keys, permissions, and delays do not satisfy declared authorizations

## 개요

1. 계정이 존재하지 않는데 트랜잭션을 발생시킨 경우
2. 계정은 존재하나 지갑안에 키가 저장되어 있지 않은 경우
3. 계정은 존재하고 지갑안에 키가 들어있으나 지갑이 잠긴 경우

위 3개의 경우에 발생되는 오류메세지 이다.

Error 3090003: Provided keys, permissions, and delays do not satisfy declared authorizations Ensure that you have the related private keys inside your wallet and your wallet is unlocked.

## 해결방법

### 1. 계정이 존재하지 않는데 트랜잭션을 발생시킨 경우

계정을 만들면 된다.

### 2. 계정은 존재하나 지갑안에 키가 저장되어 있지 않은 경우

[지갑에 키 삽입하기](../../tutorial/eos-study/wallet-create.md#undefined-2) 페이지를 참고한다.

### 3. 계정은 존재하고 지갑안에 키가 들어있으나 지갑이 잠긴 경우

[지갑 잠금 해제하기](../../tutorial/eos-study/wallet-unlock.md#2) 페이지를 참고한다.

