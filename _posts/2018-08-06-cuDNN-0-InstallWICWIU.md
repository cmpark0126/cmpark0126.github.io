---
title:  "cuDNN(0) - WICWIU LINUX GPU 버전 설치 : 필요없는 분들은 넘어가셔도 문제가 없습니다."
modified: 2018-08-06T17:00:00-:30:00
categories:
  - Develop
tags:
  - cuDNN
  - WICWIU
  - DeepLearning
  - Framework
---

이 글은 우리 연구실에서 개발한 WICWIU API를 이해시키기 위한 용도로 사용될 것이기 때문에,
일반적인 설명과는 조금 다를 것이라는 것에서 양해를 구한다.

설명에서는 WICWIU의 설명을 겸하여 진행한다.


{% include toc title="cuDNN_Host2Memory" %}

## WICWIU란?

WICWIU는 국내 대학 최초로 공개하는 딥러닝 오픈소스 프레임워크로,
나는 이 프레임워크을 설계하고 개발하는 팀의 1기로 참여하여 진행했다.

현재는 3기까지 프로젝트가 진행되었으며, 프로그램도 어느정도 규모를 가지게 되었다.
그렇기에 이 블로그 글은 개인적인 정보 정리와 함께 인수인계 자료를 겸하고자 한다.


## 왜 cuDNN을?

학부 프로젝트로 C++ 딥러닝 라이브러리를 개발하게 되었다.
라이브러리 개발에는 GPU를 지원해야 한다는 조건이 있었다.

그렇게 나는 cuDNN을 사용하게 되었다.


## cuDNN이란?

cuDNN은 nvidia gpu를 사용할 때, 특히 딥러닝 파트를 구현할 때,
거의 필수적으로 사용되고 있는 라이브러리이다.
물론 일부 라이브러리는 cuda를 이용해서 딥러닝 알고리즘을 직접 구현하기도 하지만,
평범한 나같은 개발자에게는 그게 그리 쉬운 일이 아니다.
그래서 nvidia의 슈퍼개발자들이 딥러닝에서 사용하는 기본적인 알고리즘을 구현해둔 것이 cuDNN이다.

WICWIU의 GPU 코드는 거의 대부분 cuDNN의 함수를 사용하여 구현되어 있다.


## cuDNN 라이브러리 사용준비하기 (WICWIU를 중심으로)

* 우선 cuda와 cuDNN이 서버에 설치가 되어있는지를 확인할 필요가 있다. [cuda & cuDNN 버전 확인 방법](https://crmn.tistory.com/31)

* 다음으로는 WICWIU에서 서버의 cuda와 cuDNN 버전을 지원하는지 확인할 필요가 있다. [WICWIU GitHub 주소](https://github.com/WICWIU/WICWIU)

* 위의 단계를 모두 마쳤다면 다음 코드를 '.profile'에 추가한다. (컴파일에 필요한 라이브러리의 위치를 알려주기 위해)

```yml
# set PATH so it includes user's private bin directories
PATH="$HOME/bin:$HOME/.local/bin:$PATH"

export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/cuda/lib64
export CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:/usr/local/cuda/include
export C_INCLUDE_PATH=$C_INCLUDE_PATH:/usr/local/cuda/include
export WICWIU_PATH=/home/chuniee/DLOP/Header
```

* 파일에 위의 내용을 추가했다면 이제 본격적으로 라이브러리를 실행해보자.

```yml
$ git clone https://github.com/WICWIU/WICWIU # 라이브러리 설치
$ cd WICWIC/tutorials/MNIST # tutorial 코드 위치
$ make # gcc, nvcc를 사용하여 컴파일 진행
$ ./main # 실행
```

* 프로그램이 동작한다면, 현재 cuda와 cuDNN 라이브러리를 정확하게 include하고 있다는 의미이다. 축하한다.


## 끝
WICWIU 프로젝트를 처음 시작할 때, '언젠가 이런 글을 적지 않을까'하고 1기 팀원들과 농담조로 얘기했던 적이 있다. 딱 1년 전이었다.

...감개무량하다. 한편으로는 그 많은 코드들을 어떻게 다 정리할까 걱정이 앞서기는 한다.

어디까지 해볼 수 있을지, 일단 정리해보겠다.
