---
title:  "Rust-lang/Cargo(1) - 1. Getting Started"
modified: 2019-06-29T12:00:00-:30:00
categories:
  - Rust-lang/Cargo
tags:
  - [Rust-lang, Rust-lang/Cargo]
---

* Rust 패키지 매니저인 cargo를 스터디한 내용을 정리합니다.
* Text book: https://doc.rust-lang.org/cargo/

## 1.1. Installation

### Install Rust and Cargo

Linux나 macOS을 사용하는 사람이라면 다음 명령어를 따르자

```bash
$ curl https://sh.rustup.rs -sSf | sh
...
1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
> 1 (사용자 입력)
```

위 명령어를 실행하고 올바로 Rust가 설치되면 다음 메세지를 확인할 수 있을 것이다.

```bash
Rust is installed now. Great!

To get started you need Cargo\'s bin directory ($HOME/.cargo/bin) in your PATH
environment variable. Next time you log in this will be done automatically.

To configure your current shell run source $HOME/.cargo/env
```

초기 환경 변수 설정은 직접 해줘야 한다. 보통 다음 로그인 때는 자동으로 환경변수가 적용되는데, 안되면 위의 shell 명령어를 실행시키거나 .bashrc 혹은 .profile을 아래와 같이 직접 수정하고 적용하자 (아마 자동으로 추가되어 있을 것이다)

```bash
$ vi .profile
# add 'export PATH="$HOME/.cargo/bin:$PATH"  on last line of .profile
$ source .profile
```

Window를 사용하는 사람이라면 아래 링크에서 파일을 다운받도록 하자. 링크가 다운로드가 되지 않는다면 공식페이지를 참고하여 다운로드 한다.
- [rustup-init.exe](https://win.rustup.rs/)
- 파일을 실행하면 콘솔창이 하나 뜬다. 위에서 보인 방식과 비슷한 절차를 거쳐 설치를 진행하도록 한다.
- 아마 환경 변수 설정은 신경쓰지 않아도 될 것이다.

beta 버전이나 nightly 버전, 혹은 다른 옵션으로 언어를 다운로드할 수 있다. [(공식 문서 참고)](https://doc.rust-lang.org/cargo/getting-started/installation.html)

### Build and Install Cargo from Source

[Source 코드](https://github.com/rust-lang/cargo#compiling-from-source)를 사용해서 직접 설치하는 것도 가능하다.


## 1.2. First Step with cargo

새 패키지는 아래와 같은 방법으로 생성한다.
- binary (application) 프로그램용 패키지 생성 (아래 명령어에서 --bin은 default 값으로 생략되어 있다.)
```bash
$ cargo new hello_world # 또는 cargo new hello_world --bin
    Created binary (application) `hello-world` package
```

- library 작성용 패키지 생성
```bash
$ cargo new hello_world_lib --lib
    Created library `hello-world_lib` package
```

library 패키지는 다음에 확인하고, 우선 binary package를 확인해보자.
```bash
$ cd hello_world
$ tree .
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```

- Cargo.toml
    - manifest라고 불리며, 이는 Cargo가 패키지를 컴파일하는데 필요한 모든 metadata를 포함하고 있다.

- src/main.rs
    - 기본적으로 "Hello, world!"라고 하는 간단한 문구를 출력하기 위한 rust 프로그램이 짜여져 있다. (default)

그럼 이 바이너리 패키지를 컴파일 하는 단계를 확인해보자
- 컴파일
```bash
$ cargo build
    Compiling hello_world v0.1.0 (~~~)
     Finished dev [unoptimized + debuginfo] target(s) in 0.54s
```

- 프로그램 실행
```bash
$ ./target/debug/hello_world
Hello, world!
```

- 컴파일과 프로그램 실행을 순서대로 한번에 진행
```bash
$ cargo run
    Compiling hello_world v0.1.0 (~~~)
     Finished dev [unoptimized + debuginfo] target(s) in 0.54s
      Running `target/debug/hello_world`
Hello, world!
```

### Going further
다음 챕터인 [Cargo Guide](https://doc.rust-lang.org/cargo/guide/index.html) 확인
- [한글 버전 Cargo Guide]()
