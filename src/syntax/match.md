# match

> [!NOTE] 
> match เป็นโครงสร้างควบคุมที่ใช้ในการจับคู่รูปแบบ (pattern matching) ใน Rust มันช่วยให้เราสามารถเปรียบเทียบค่ากับรูปแบบต่างๆ และดำเนินการตามรูปแบบที่ตรงกัน match มีความยืดหยุ่นและมีประสิทธิภาพสูง เหมาะสำหรับการจัดการกับค่าที่มีหลายรูปแบบหรือกรณีต่างๆ

## ตัวอย่าง:
- การใช้ match กับตัวเลข
```rust, editable
fn main() {
    let number = 13;

    match number {
        0 => println!("ศูนย์"),
        1 | 2 => println!("หนึ่งหรือสอง"),
        3..=9 => println!("สามถึงเก้า"),
        _ => println!("มากกว่าเก้า"),
    }
}
```

- การใช้ match กับ enum
```rust, editable
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {
    let coin = Coin::Dime;
    println!("มูลค่าของเหรียญ: {} เซนต์", value_in_cents(coin));
}
```

- การใช้ match กับ enum กรณี function
```rust, editable
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn process_message(msg: Message) {
    match msg {
        Message::Quit => {
            println!("ออกจากโปรแกรม");
        }
        Message::Move { x, y } => {
            println!("เคลื่อนที่ไปยังตำแหน่ง x: {}, y: {}", x, y);
        }
        Message::Write(text) => {
            println!("ข้อความ: {}", text);
        }
        Message::ChangeColor(r, g, b) => {
            println!("เปลี่ยนสีเป็น RGB({}, {}, {})", r, g, b);
        }
    }
}

fn main() {
    let messages = vec![
        Message::Move { x: 10, y: 20 },
        Message::Write(String::from("สวัสดี")),
        Message::ChangeColor(255, 0, 0),
        Message::Quit
    ];

    for msg in messages {
        process_message(msg);
    }
}
```

- การใช้ match กับ Option
```rust, editable
fn main() {
    let some_number = Some(5);

    match some_number {
        Some(n) => println!("ค่าคือ: {}", n),
        None => println!("ไม่มีค่า"),
    }
}
```

## โจทย์:

##### ⭐️
1. เติม match expression ให้สมบูรณ์เพื่อแปลงตัวเลขเป็นคำอ่านภาษาไทย (1-5)

```rust, editable
fn number_to_thai(num: u32) -> &static str {
    match ___ {
        1 => "หนึ่ง",
        ___ => "สอง",
        3 => ___,
        ___ => "สี่",
        5 => "ห้า",
        _ => "ไม่รู้จัก",
    }
}

fn main() {
    println!("{}", number_to_thai(3));
}
```

2. เติม match expression ให้สมบูรณ์เพื่อตรวจสอบว่าตัวอักษรเป็นสระหรือพยัญชนะ (a, e, i, o, u เป็นสระ)

```rust, editable
fn vowel_or_consonant(c: char) -> &static str {
    match ___ {
        'a' | ___ | 'i' | ___ | 'u' => "สระ",
        'a'..='z' => ___,
        _ => "ไม่ใช่ตัวอักษร",
    }
}

fn main() {
    println!("{}", vowel_or_consonant('b'));
}
```

##### ⭐️⭐️
1. เติม match expression ให้สมบูรณ์เพื่อคำนวณค่า factorial ของตัวเลข 0-5 (ใช้ recursive)

```rust, editable
fn factorial(n: u32) -> u32 {
    match ___ {
        0 | 1 => ___,
        2 => 2,
        3 => ___,
        4 => 24,
        5 => ___,
        _ => panic!("ไม่รองรับตัวเลขนี้"),
    }
}

fn main() {
    println!("5! = {}", factorial(5));
}
```

2. เติม match expression ให้สมบูรณ์เพื่อแปลงเกรดเป็นคะแนน (A=4, B=3, C=2, D=1, F=0)

```rust, editable
enum Grade {
    A, B, C, D, F
}

fn grade_to_points(grade: Grade) -> f32 {
    match ___ {
        Grade::A => ___,
        ___ => 3.0,
        Grade::C => 2.0,
        ___ => ___,
        Grade::F => 0.0,
    }
}

fn main() {
    println!("คะแนนของเกรด B: {}", grade_to_points(Grade::B));
}
```

##### ⭐️⭐️⭐️
1. เติม match expression ให้สมบูรณ์เพื่อวิเคราะห์โครงสร้างข้อมูลแบบต้นไม้ (binary tree)

```rust, editable
enum BinaryTree {
    Leaf(i32),
    Node(Box<BinaryTree>, i32, Box<BinaryTree>),
}

fn sum_tree(tree: &BinaryTree) -> i32 {
    match ___ {
        BinaryTree::Leaf(value) => ___,
        BinaryTree::Node(left, value, right) => {
            ___ + value + ___
        }
    }
}

fn main() {
    let tree = BinaryTree::Node(
        Box::new(BinaryTree::Leaf(1)),
        2,
        Box::new(BinaryTree::Node(
            Box::new(BinaryTree::Leaf(3)),
            4,
            Box::new(BinaryTree::Leaf(5))
        ))
    );
    println!("ผลรวมของต้นไม้: {}", sum_tree(&tree));
}
```

2. เติม match expression ให้สมบูรณ์เพื่อประมวลผลคำสั่งของเครื่องคิดเลขอย่างง่าย

```rust, editable
enum Operation {
    Add(f64, f64),
    Subtract(f64, f64),
    Multiply(f64, f64),
    Divide(f64, f64),
}

fn calculate(op: Operation) -> Result<f64, &static str> {
    match ___ {
        Operation::Add(a, b) => Ok(___),
        Operation::Subtract(a, b) => ___,
        ___ => Ok(a * b),
        Operation::Divide(a, b) => {
            if b == 0.0 {
                ___
            } else {
                ___
            }
        }
    }
}

fn main() {
    let result = calculate(Operation::Divide(10.0, 2.0));

    match result {
        Ok(value) => println!("ผลลัพธ์: {}", value),
        Err(msg) => println!("เกิดข้อผิดพลาด: {}", msg),
    }
}
```
