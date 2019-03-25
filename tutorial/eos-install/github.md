# Github로 설치하기

## 1. github 코드를 내려 받는다.

최신버전의 EOSIO 코드를 내려 받는다. 터미널 창을 열어서 아래와 같이 입력한다.

```text
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

### 1.7.0 이전 버전의 경우

```text
cd eos
./eosio_build.sh
```

### 1.7.0 이후 버전의 경우

```text
cd eos
./scripts/eosio_build.sh
```

> ```text
>         Home Brew installation found @
>         /usr/local/bin/brew
>
>         Checking dependencies.
>         Checking automake ...            automake NOT found.
>         Checking Libtool ...             Libtool NOT found.
>         Checking OpenSSL ...             OpenSSL NOT found.
>         Checking llvm ...                llvm NOT found.
>         Checking wget ...                wget NOT found.
>         Checking CMake ...               CMake NOT found.
>         Checking GMP ...                 GMP NOT found.
>         Checking gettext ...             gettext NOT found.
>         Checking MongoDB ...             MongoDB NOT found.
>         Checking Doxygen ...             Doxygen NOT found.
>         Checking Graphviz ...            Graphviz NOT found.
>         Checking LCOV ...                LCOV NOT found.
>         Checking Python3 ...             python3 NOT found.
>
>         The following dependencies are required to install EOSIO.
>
>         1. automake
>         2. Libtool
>         3. OpenSSL
>         4. llvm
>         5. wget
>         6. CMake
>         7. GMP
>         8. gettext
>         9. MongoDB
>         10. Doxygen
>         11. Graphviz
>         12. LCOV
>         13. Python 3
>
>
> Do you wish to install these packages?
> 1: YES
> 2: NO
>
> ```

위 화면이 표시 될 경우 1을 누르고 Enter를 누르면 된다. 참고로 빌드가 완료되기 까지 시간은 컴퓨터 사양에 따라 다르지만 3시간 정도 소모된다. 빌드 과정이 끝났으면 아래 install script를 추가로 실행한다.

```text
sudo ./eosio_install.sh
```

그러면 모든 설치가 완료된다. 참고로 오픈 초기에는 CMakeLists 가 잘못 선언되어 있는경우가 많아 공식 깃허브에서 받은 코드임에도 불구하고 정상적으로 빌드가 되지 않는 문제가 자주 일어났다. 지금은 대부분 해결되었다.

