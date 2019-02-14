# 지갑 만들기

## 개요

지갑을 생성하고 키를 삽입하는 방법에 대하여 학습한다.

블록체인에서 말하는 지갑\( wallet \) 은 우리가 일상생활에서 사용하는 지갑의 개념과는 거리가 멀다. 처음 블록체인에 관하여 개념을 익힐 때 헷갈려 하는 부분이 바로 지갑의 개념인데 지갑을 코인을 보관하는 장소라고 착각하는 경우가 많기 때문이다. 이오스뿐만 아니라 대부분의 블록체인에서 말하는 지갑의 개념은 아래와 같다.

{% hint style="info" %}
지갑은 **키 저장소**를 의미한다.
{% endhint %}

여기서 말하는 키 \( key \) 란 실제 이오스 상에서 비밀번호 대체 개념으로 사용하는 암호라고 생각하면 된다. 알고리즘 방식은 비대칭키 암호 방식을 사용하는데, 우리가 잘 알고 있는 RSA 방식이 아닌 [ECC](../../keywords/e/ecc.md) 알고리즘을 사용한다. 지갑에 대해 좀더 자세히 알고 싶다면 [keosd](../../keywords/k/keosd.md) 페이지를 참고하길 바란다.

## 지갑 만들기

최초로 EOS를 구동하면 가장 먼저 해야 할 것은 바로 지갑을 생성하는 것이다. 지갑을 생성하지 않으면 계정을 생성하거나 토큰을 발행하는 등 모든 계약을 사용할 수 없기 때문이다.

### 1. 지갑 생성 Command 입력

```text
cd ~/eos/build/programs/cleos
./cleos wallet create --to-console
```

{% hint style="info" %}
​[Github로 설치하기](https://eosdev.wiki/~/drafts/-LU4_aLi8LNpm55ManKR/primary/tutorial/eos-install/github) 페이지에서 sudo ./eosio\_install.sh 스크립트를 실행했었다면 디렉터리로 이동하지 않고 전역으로 cleos라는 커맨드만 입력해도 동일하게 동작한다. 그러나 초반에는 eos의 PATH를 익히기 위하여 직접 이동하여 동작하는 습관을 기르도록 하자. 자동 쉘 스크립트 기능은 나중에 익숙해진 이후에 사용하는 것을 추천한다.
{% endhint %}

### 2. 지갑 비밀번호 저장하기

위와 같이 지갑을 생성하면 아래와 같은 콘솔 메세지 결과를 얻을 수 있다.

> ```text
> Creating wallet: default
> Save password to use in the future to unlock this wallet.
> Without password imported keys will not be retrievable.
> "PW5KEaEmxsKXpwRok3LsnjbVBdsUWSame8wdoqpGMrtvi1d8AsJiR"
> ```

가장 하단에 53글자의 지갑 패스워드를 발급 받을 수 있다. 지갑 패스워드는 **분실하면 다시는 얻을 수 없으니** 안전한곳에 저장을 하도록 하자.

## 지갑에 키 삽입하기

### 1. 랜덤 키 생성하기

```text
./cleos create key --to-console
```

> ```text
> Private key: 5K2FoaWSZHYjfhXgcGJ1ojhBN6F2ZrUM66qqHZsAB1RCEV35E27
> Public key: EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ
> ```
>
> ```text
> Private key: 5K2g7zP1Gbz33TXZ3Y9RFqBKfmAt3gdrqPrBCNLNgMZbP54MPtk
> Public key: EOS6muMvKhjH2Y5A3LgytzR8D9sTVtAreCr42f8JNYxarjX8pa3uM
> ```

랜덤으로 생성된 key를 얻을 수 있다. 2개를 생성해 보자. 참고로 키를 분실하게 되면 **복구할 수 있는 방법이 없으니** 잘 보관하도록 하자.

### 2. 생성한 키를 지갑에 삽입하기

```text
./cleos wallet import
```

위 커맨드를 입력 한 다음 위에서 발행한 **private key**를 삽입한다. public key와 **혼동**하지 말자.

> ```text
> private key: imported private key for: EOS8N1AWn6pXrKG4cyCCWYvZQU8Z4P1HCmhGKeGqRWwfe8z8j6PYJ
> ```
>
> ```text
> private key: imported private key for: EOS6muMvKhjH2Y5A3LgytzR8D9sTVtAreCr42f8JNYxarjX8pa3uM
> ```

정상적으로 삽입된 것을 볼 수 있다.

## 이름있는 지갑 생성하기

[지갑 만들기](wallet-create.md#1-command) 에서 입력한 방법은 지갑의 이름을 지정하지 않았기 때문에 디폴트 이름을 가진 지갑을 생성한 것이다. 일반적인 환경에서는 디폴트 지갑으로 사용해도 굳이 문제 될 것은 없다. 그러나 지갑을 여러개 생성하여 관리하고 싶다면 직접 이름을 지정하여 관리하는것이 좋다.

### 1. testkeys 라는 이름으로 지갑 생성하기

```text
./cleos wallet create -n testkeys --to-console
```

> ```text
> Creating wallet: testkeys
> Save password to use in the future to unlock this wallet.
> Without password imported keys will not be retrievable.
> "PW5KDVq3ZfPh1gxzcqtM5yUdphwoVtK4hwEL5cZCzqXEhWjvbQiaU"
> ```

testkeys 라는 이름의 지갑이 정상적으로 생성 된것을 볼 수 있다.

### 2. 생성한 키를 이름있는 지갑에 삽입하기

```text
cleos wallet import -n testkeys
```

삽입시에는 반드시 private key를 넣어야 한다. public key와 혼동하지 않도록 한다.

## 지갑 저장소 위치

```text
cd ~
cd eosio-wallet/
ls
```

> ```text
> config.ini      default.wallet  keosd.sock      testkeys.wallet wallet.lock
> ```

지갑 저장소 Path를 따로 건드리지 않았다면 기본적으로 홈 디렉터리 아래 eosio-wallet/ 디렉터리가 생성되었을 것이다. 여기에 보면 방금 생성했던 default.wallet 과 testkeys.wallet 파일이 추가적으로 생성돼 것을 볼 수 있다. 다음 편에서는 지갑의 보안을 한층 더 강화시켜주는 lock, unlock 그리고 자동잠금을 늘릴 수 있는 환경설정에 관한 방법에 대해서 알아보도록 하자

