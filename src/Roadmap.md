# Roadmap

## 1. ทบทวน (10:00-10:10น.) (โอปอล)
- cargo command (add กับ install ต่างกันยังไง)
  - install
  - add
  - remove
  - init
  - run
- vscode extension (ย้ำเตือนว่าต้องติดตั้งก่อน)
  - rust-analyzer
  - dependi
  - even better toml

## 2. Init Project (10:10-10:30) (โอปอล)
- Init project ผ่าน cargo init
- verify โดย cargo run project ได้คำว่า hello world
- อธิบาย Structure ของ Rust
  - folder / file ที่จำเป็น
    - src/
    - main.rs
    - function main()
    - lib.rs
    - mod.rs
  - module คืออะไร
  - วิธีสร้าง file/folder ใหม่ + วิธี public + วิธี use
  - Cargo.toml / Cargo.lock
    - อธิบายรายละเอียดของ Cargo.toml
  - targets/
  - tests/ (optional)
  - crate คืออะไร
  - features toggle (อธิบายแค่หลักการ และวิธีใช้งาน ยังไม่สอนวิธี implement)
  - rustfmt (optional)
- break 5นาที

## 3. Syntax พื้นฐาน (เก่ง)
- println! & dbg!
- variable
  - let
  - const
  - static
- Stack & Heap & Static
- lifetime (Optional)
- size limit (Optional)
- ใคร cleanup
- performance (Optional)
- types (จบช่วงเช้า)
  - Int (Signed vs Unsigned)
    - u8 vs i8 → u8: 0 - (2^8)-1  vs i8: หักออก 1 bit เพื่อเก็บ Sign(+/-) -(2^7) - (2^7)-1
  - Char
  - &str
    - อธิบายคร่าวๆก่อน แล้วค่อยยกตัวอย่างปัญหาตอนเรื่อง Ownership & Borrowing
  - Array vs Vector
  - String
  - Tuple
    - ต่างจาก Array ตรงที่สามารถมีหลาย Type ได้
  - struct
  - enum
  - Option<T>
  - Result<T, E>
  - mutable

- พักเที่ยง (11:30 - 13:00)

## ช่วงบ่าย (13:00 - 17:00)
### Syntax พื้นฐาน (ต่อ) 
- Logic syntax (เหน่ง)
  - [if syntax](./syntax/if.md)
    - if
    - if let
  - [loop syntax](./syntax/loop.md)
    - while
    - while let
    - for
    - loop
    - break
  - [match syntax](./syntax/match.md)
  - [function syntax](./syntax/function.md)
    - function signature
  - [Error Handling](./syntax/error_handling.md)
    - handle Result<R, E>
    - handle Option<T>
    - Panic! & unwrap

- พัก (10 นาที) 

## Ownership & Borrowing (โอปอล)
- move semantics
- reference (borrow)
- drop
- lifetime
- impl & trait
- dynamic dispatch
- macro (ไม่สอนวิธีเขียน)
  - macro มี 2 ประเภท - macro! กับ #[macro]
- clone
- debug
- display
- JSON
  - Serialize
  - Deserialize
- Async Runtime
  - Tokio → tokio::main, async/await
  - Async Trait
- generic (optional)
  - generic type & function
- Singleton (Optional)
  - OnceLock / LazyLock

- พัก (10 นาที)

## Workshop (1 ชั่วโมง) (โอปอล)
- สร้าง Axum Service
  - Basic (1 ชั่วโมง)
    - route GET / helloworld
    - extract Query, Param, Body
    - response json + status code
    - response error
  - Advance (Optional)
    - CRUD Mongo