# bad alloc

##  개요

램이 부족할때 나타나는 오류

## 증상

```text
warn  2019-06-01T10:32:36.472 thread-0  controller.cpp:238            emit                 ] bad alloc
error 2019-06-01T10:32:41.989 thread-0  main.cpp:132                  main                 ] bad alloc
```

대부분 bad alloc이 발생하는 경우는 chain-state-db-size 값 보다 state db 사이즈가 늘어남에 따라 더이상 shared\_memory 할당이 불가능 할 때 발생 한다.

## 해결방법

궁극적인 해결 방안은 물리적인 RAM 용량을 늘리면 된다.

