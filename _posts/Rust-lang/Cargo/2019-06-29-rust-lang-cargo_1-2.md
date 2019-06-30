---
title:  "Ch1. Getting Started(2) - First Step with cargo"
modified: 2019-06-29T12:00:00-:30:00
categories:
  - Rust-lang/Cargo
tags:
  - [Rust-lang, Rust-lang/Cargo]
---

* Rust 패키지 매니저인 cargo를 스터디한 내용을 정리합니다.
* Text book: https://doc.rust-lang.org/cargo/

### First Step with cargo

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
