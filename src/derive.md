- [Derive Macro](#derive-macro)
  - [Debug](#debug)
  - [Example Derive Debug](#example-derive-debug)
  - [Clone](#clone)
      - [Example Derive Clone](#example-derive-clone)
  - [Copy](#copy)
      - [Example Derive Copy](#example-derive-copy)
  - [PartialEq](#partialeq)
      - [Example Derive PartialEq](#example-derive-partialeq)
  - [Eq](#eq)
      - [Example Derive Eq](#example-derive-eq)
  - [PartialOrd](#partialord)
      - [Example Derive PartialOrd](#example-derive-partialord)
  - [Ord](#ord)
      - [Example Derive Ord](#example-derive-ord)
  - [Default](#default)
      - [Example Derive Default](#example-derive-default)

# Derive Macro

> [!NOTE]
>
> - `Derive Macro` คือ `procedural macro` ชนิดหนึ่ง
> - `Derive Macro` คือ shorthand impl Trait ให้กับตัวแปรชนิดต่างๆ เช่น struct หรือ enum
>   โดยที่เราไม่ต้องเขียน impl Trait ด้วยตัวเอง
> - `Derive Macro` ที่ได้ใช้บ่อยๆ มีดังนี้
>   - `Debug`
>   - `PartialEq`
>   - `Eq`
>   - `PartialOrd`
>   - `Ord`
>   - `Clone`
>   - `Copy`
>   - `Default`

> [!WARNING]
>
> การ Derive ความสามารถให้กับ struct หรือ enum เกินความจำเป็นจะทำให้มีผลกระทบต่อ
> Performance เนื่องจากมีการ Allocate/Deallocate Heap Memory ที่สูงตามมา

## Debug

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการ debug ค่าในตัวแปร เช่น struct หรือ enum ผ่าน
> `println!("{:?}", value)` หรือ `dbg!(value)` โดยที่เราไม่ต้องเขียน impl Debug
> ด้วยตัวเอง

## Example Derive Debug

```rust, editable
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {:?}", &rect1);
    // หรือ
    dbg!(&rect1);
}
```

## Clone

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการ Clone ค่าของ struct หรือ enum ไปสร้างตัวแปรใหม่ ผ่าน
> method `.clone()`

> [!TIP]
> การ Clone จะทำให้ตัวแปรที่ถูก Clone มีค่าเหมือนตัวแปรต้น แต่เป็นตัวแปรใหม่ ที่มี Ownership
> เป็นของตัวเอง

#### Example Derive Clone

```rust, editable
#[derive(Clone)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    let rect2 = rect1.clone();

    // react1 จะยังสามารถใช้งานได้ เนื่องจากไม่มีการย้าย Ownership
    println!("rect1: {:?}", rect1);
    println!("rect2: {:?}", rect2);
}
```

## Copy

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการ Clone ค่าของ struct หรือ enum ไปยังตัวแปรอื่น
> **<u>โดยอัตโนมัติ</u>** โดยไม่ใช้ `Move Semantics` (เหมือน Primitive Types)

> [!WARNING]
>
> - ต้องใช้คู่กับ Derive `Clone` พร้อมกันเท่านั้น
> - ใช้เมื่อจำเป็นเท่านั้น เนื่องจากมี Cost ในการ Allocate/Deallocate Heap Memory ที่สูงตามมา
>   ทำให้มีผลกระทบต่อ Performance

#### Example Derive Copy

```rust, editable
#[derive(Clone, Copy)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    // rect1 จะถูก Copy ไปยัง rect2 โดยอัตโนมัติ โดยไม่ต้องใช้ method `.clone()`
    // ซึ่งทำให้ rect1 ยังสามารถใช้งานได้ เนื่องจากไม่มีการย้าย Ownership
    let rect2 = rect1;

    // rect1 จะยังสามารถใช้งานได้ เนื่องจากไม่มีการย้าย Ownership
    println!("rect1: {:?}", rect1);
    println!("rect2: {:?}", rect2);
}
```

## PartialEq

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการเปรียบเทียบ **<u>ค่าของ key</u>** ใน struct หรือ enum
> **<u>ทีละคู่</u>** ผ่าน `==` หรือ `!=`

#### Example Derive PartialEq

```rust, editable
#[derive(PartialEq)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    let rect2 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1.width == rect2.width: {}", rect1.width == rect2.width);
    println!("rect1.height == rect2.height: {}", rect1.height == rect2.height);
}
```

## Eq

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการเปรียบเทียบค่าของ struct หรือ enum **<u>ทั้งหมด</u>** ผ่าน
> `==` หรือ `!=`

> [!WARNING]
> ต้องใช้คู่กับ Derive `PartialEq` พร้อมกันเท่านั้น

#### Example Derive Eq

```rust, editable
#[derive(PartialEq, Eq)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    let rect2 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 == rect2: {}", rect1 == rect2);
}
```

## PartialOrd

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการเปรียบเทียบ **<u>ค่าของ key</u>** ใน struct หรือ enum
> **<u>ทีละคู่</u>** ผ่าน `<`, `>`, `<=`, `>=`

#### Example Derive PartialOrd

```rust, editable
#[derive(PartialEq, PartialOrd)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    let rect2 = Rectangle {
        width: 20,
        height: 40,
    };

    println!("rect1.width < rect2.width: {}", rect1.width < rect2.width);
    println!("rect1.height >= rect2.height: {}", rect1.height >= rect2.height);
}
```

## Ord

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการเปรียบเทียบค่าของ struct หรือ enum **<u>ทั้งหมด</u>** ผ่าน
> `<`, `>`, `<=`, `>=`

> [!WARNING]
> ต้องใช้คู่กับ Derive `PartialOrd` พร้อมกันเท่านั้น

#### Example Derive Ord

```rust, editable
#[derive(PartialEq, PartialOrd, Eq, Ord)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    let rect2 = Rectangle {
        width: 20,
        height: 40,
    };

    println!("rect1 < rect2: {}", rect1 < rect2);
    println!("rect1 > rect2: {}", rect1 > rect2);
}
```

## Default

> [!NOTE]
> ใช้สำหรับเพิ่มความสามารถในการสร้าง struct หรือ enum
> ตัวใหม่ให้มีค่าเป็นค่าเริ่มต้นของตัวแปรชนิดต่างๆ ผ่าน method `::default()`

#### Example Derive Default

```rust, editable
#[derive(Default)]
struct Rectangle {
    width: u32,
    height: u32,
}

// หากเป็น enum จำเป็นต้องกำหนดค่า default เองด้วย `#[default]` attribute
#[derive(Debug, Default, PartialEq)]
enum Test {
    A,
    #[default]
    // กำหนดให้ B เป็นค่า default ของ enum Test
    B,
    C,
}

fn main() {
    let rect1 = Rectangle::default();
    let test_enum = Test::default();
    
    assert_eq!(rect1.width, 0);
    assert_eq!(rect1.height, 0);
    assert_eq!(test_enum, Test::B);
}
```
