# if

> [!NOTE] 
> เป็นโครงสร้างควบคุมที่ใช้ในการตัดสินใจว่าจะทำงานส่วนใดของโค้ดขึ้นอยู่กับเงื่อนไขที่กำหนด ใน Rust, if มีลักษณะคล้ายกับภาษาโปรแกรมอื่นๆ แต่มีจุดเด่นคือไม่จำเป็นต้องใส่วงเล็บรอบเงื่อนไข และบล็อกโค้ดต้องอยู่ในวงเล็บปีกกาเสมอ

ตัวอย่างการใช้ if:

```rust, editable
fn main() {

    let x = 5; // ลองเปลี่ยนค่า x เป็นจำนวนลบดู

    if x > 0 {
        println!("x เป็นจำนวนบวก");
    } else if x < 0 {
        println!("x เป็นจำนวนลบ");
    } else {
        println!("x เป็นศูนย์");
    }
}
```

# if let

> [!NOTE]
> if let เป็นรูปแบบพิเศษของ if ที่ใช้สำหรับการจับคู่รูปแบบ (pattern matching) แบบง่าย โดยเฉพาะอย่างยิ่งเมื่อต้องการตรวจสอบค่าเพียงค่าเดียวจาก enum หรือ Option โดยไม่ต้องใช้ match ที่ยาวเกินไป

- ก่อนหน้าใช้ if let ต้องใช้ match ก่อน
```rust, editable
fn main() {
    let some_value: Option<i32> = Some(3);

    match some_value {
        Some(x) => println!("ค่าภายใน Some คือ: {}", x),
        None => println!("ไม่มีค่า"),
    }
}
```
> [!TIP]
> ถ้าเราไม่ต้องการใช้ค่าที่อยู่ใน Option ก็สามารถใช้ if let แทน match ได้เลย

ตัวอย่างการใช้ if let:

```rust, editable
fn main() {

    let some_value: Option<i32> = Some(3); //ลองเปลี่ยนค่า some_value เป็น None ดู

    if let Some(x) = some_value {
        println!("ค่าภายใน Some คือ: {}", x);
    } else {
        println!("ไม่มีค่า");
    }
}
```

## โจทย์:

##### ⭐️
เติมโครงสร้าง if ให้สมบูรณ์เพื่อตรวจสอบว่าตัวเลขเป็นบวก ลบ หรือศูนย์

```rust, editable
fn main() {

    let number = -5;

    __ number > 0 {
        println!("เป็นจำนวนบวก");
    } __ number < 0 {
        println!("เป็นจำนวนลบ");
    } __ {
        println!("เป็นศูนย์");
    }
}
```

##### ⭐️⭐️

เติมโครงสร้าง if let ให้สมบูรณ์เพื่อตรวจสอบค่าใน Option

```rust, editable
fn main() {
    let maybe_number: __ = Some(42);

    if ____ {
        println!("ค่าภายใน Option คือ: {}", n);
    } else {
        println!("ไม่มีค่า");
    }
}
```

##### ⭐️⭐️⭐️

เติมโครงสร้าง if และ if let ให้สมบูรณ์เพื่อตรวจสอบประเภทของยานพาหนะและจำนวนล้อ

```rust, editable
enum Vehicle {
    Car(u8),
    Bicycle,
    Boat,
}

fn main() {

    let vehicle = Vehicle::Car(4);
    
    if let ________ {
        if wheels == 4 {
            println!("เป็นรถยนต์ 4 ล้อ");
        } else {
            println!("เป็นรถยนต์ที่มีจำนวนล้อไม่ปกติ: {} ล้อ", wheels);
        }
    } else if let ________ = vehicle {
        println!("เป็นจักรยาน");
    } else {
        println!("เป็นเรือ");
    }
}
```
