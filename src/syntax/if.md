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

ตัวอย่างการใช้ if กับ &str และ String

```rust, editable
fn main() {
    let name: &str = "Rust";  // ใช้ &str แทน String สำหรับค่าคงที่

    if name == "Rust" {
        println!("ชื่อตรงกับ Rust");
    } else {
        println!("ชื่อไม่ตรงกับ Rust");
    }

    if name.starts_with("R") {
        println!("ชื่อขึ้นต้นด้วยตัว R");
    }

    if name.len() > 3 {
        println!("ชื่อมีความยาวมากกว่า 3 ตัวอักษร");
    }

    let empty_name: &str = "";
    if empty_name.is_empty() {
        println!("ชื่อว่างเปล่า");
    }

    // ตัวอย่างการใช้ String
    let dynamic_name = String::from("Rustacean");
    if dynamic_name.contains("Rust") {
        println!("ชื่อมีคำว่า Rust อยู่ด้วย");
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
