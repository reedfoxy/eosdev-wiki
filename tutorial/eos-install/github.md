# Github로 설치하기

## 1. github 코드를 내려 받는다.

최신버전의 EOSIO 코드를 내려 받는다. 터미널 창을 열어서 아래와 같이 입력한다.

```
cd ~
git clone https://github.com/EOSIO/eos --recursive
```

{% hint style="info" %}
정상적으로 동작하지 않는다면 git을 설치해야 한다. git을 설치하는 방법에 대해서는 이미 많이 알려져 있으므로 다루지 않는다.
{% endhint %}

{% hint style="info" %}
EOS는 약 9개의 서브 모듈을 가지고 있고, 서브 모듈 안에 또 다른 서브 모듈도 있다. 그렇기 때문에 recursive 옵션을 반드시 사용하여 서브 모듈을 함께 내려받아야 한다. 만약 실수로 해당 옵션을 넣지 않았다면 내려받은 디렉터리로 이동하여 git submodule update --init --recursive 입력하면 서브 모듈을 다시 다운로드할 수 있다. 서브모듈을 함께 내려받지 않는다면 빌시 오류가 발생한다. 만약 Mac OS을 쓴다면 Xcode를 미리 설치한 뒤 eos를 빌드 하게 되면 설치시간을 좀 더 단축할 수 있다.
{% endhint %}

## 2. 자동 빌드 스크립트를 실행한다.

eos 구동에 필요한 각종 프로그램이 함께 설치된다. 

```text
cd eos
./eosio_build.sh
```

최초 설치의 경우 컴퓨터 사양에 따라 다르지만 3시간 정도 소모된다. 빌드 과정이 끝났으면 아 install script를 추가로 실행한다.

```text
sudo ./eosio_install.sh
```

그러면 모든 설치가 완료된다. 참고로 오픈 초기에는 CMakeLists 가 잘못 선언되어 있는경우가 많아 공식 깃허브에서 받은 코드임에도 불구하고 정상적으로 빌드가 되지 않는 문제가 자주 일어났다. 지금은 대부분 해결되었다.

