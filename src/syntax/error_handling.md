# Error Handling

> [!NOTE]
> การจัดการข้อผิดพลาดใน Rust มีหลายวิธี
> ซึ่งช่วยให้เราสามารถจัดการกับสถานการณ์ที่ไม่คาดคิดได้อย่างปลอดภัยและมีประสิทธิภาพ

# Handle Result<R, E>

> [!NOTE]
> Result<R, E> เป็น enum ที่ใช้สำหรับการจัดการกับฟังก์ชันที่อาจเกิดข้อผิดพลาดได้ โดย R
> คือประเภทของค่าที่ถูกต้อง และ E คือประเภทของข้อผิดพลาด

ตัวอย่าง:

```rust, editable
use std::fs::File;

fn main() {
    let file_result = File::open("example.txt");
    
    match file_result {
        Ok(file) => println!("เปิดไฟล์สำเร็จ"),
        Err(error) => println!("เกิดข้อผิดพลาด: {:?}", error),
    }
}
```

# Handle Option<T>

> [!NOTE]
> Option<T> เป็น enum ที่ใช้เมื่อค่าอาจมีหรือไม่มีก็ได้ โดย T คือประเภทของค่าที่อาจมี

ตัวอย่าง:

```rust, editable
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    let first = numbers.first();
    
    match first {
        Some(value) => println!("ค่าแรกคือ: {}", value),
        None => println!("ไม่มีค่าในเวกเตอร์"),
    }
}
```

# ? operator

> [!NOTE]
> ? operator เป็นตัวดำเนินการที่ใช้กับ Result หรือ Option ใน Rust ซึ่งจะคืนค่าถ้าสำเร็จ หรือคืนค่าข้อผิดพลาดถ้าล้มเหลว

ตัวอย่าง:

```rust, editable
use std::fs::File;
use std::io::{self, Read};

fn read_file_contents(path: &str) -> Result<String, io::Error> {
    let mut file = File::open(path)?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}

fn main() {
    match read_file_contents("example.txt") {
        Ok(contents) => println!("ไฟล์มีเนื้อหา: {}", contents),
        Err(error) => println!("เกิดข้อผิดพลาดในการอ่านไฟล์: {:?}", error),
    }
}
```

> [!TIP]
> การใช้ `?` operator ช่วยให้โค้ดสั้นลงและอ่านง่ายขึ้น เมื่อเทียบกับการใช้ `match` หรือ `unwrap()`

ตัวอย่างเดียวกันแต่ไม่ใช้ ? operator:

```rust, editable
use std::fs::File;
use std::io::{self, Read};

fn read_file_contents(path: &str) -> Result<String, io::Error> {
    let mut file = match File::open(path) {
        Ok(file) => file,
        Err(error) => return Err(error),
    };
    
    let mut contents = String::new();
    match file.read_to_string(&mut contents) {
        Ok(_) => Ok(contents),
        Err(error) => Err(error),
    }
}

fn main() {
    match read_file_contents("example.txt") {
        Ok(contents) => println!("ไฟล์มีเนื้อหา: {}", contents),
        Err(error) => println!("เกิดข้อผิดพลาดในการอ่านไฟล์: {:?}", error),
    }
}
```

# Panic! & unwrap

> [!NOTE]
> panic! เป็นมาโครที่ใช้เมื่อเกิดข้อผิดพลาดที่ไม่สามารถกู้คืนได้ ส่วน unwrap() เป็นเมธอดที่ใช้กับ
> Result หรือ Option ซึ่งจะคืนค่าถ้าสำเร็จ หรือ panic! ถ้าล้มเหลว

ตัวอย่าง:

```rust, editable
fn main() {
    let x: Option<i32> = Some(5);
    let y: Option<i32> = None;
    
    println!("ค่าของ x: {}", x.unwrap());
    println!("ค่าของ y: {}", y.unwrap()); // จะเกิด panic!
}
```

ตัวอย่าง:

```rust, editable
fn main() {
    let x: Result<i32, &str> = Ok(5);
    let y: Result<i32, &str> = Err("ข้อผิดพลาดที่เกิดขึ้น");
    
    println!("ค่าของ x: {}", x.unwrap_or(0));
    println!("ค่าของ y: {}", y.unwrap_or_else(|e| {
        println!("เกิดข้อผิดพลาด y: {}", e);
        0 // ค่าเริ่มต้นถ้าเกิดข้อผิดพลาด
    }));
}
```
> [!TIP]
> `unwrap_or()` ซึ่งเป็นวิธีที่สั้นกว่าในการจัดการกับ Result หรือ Option

> [!TIP]
> `unwrap_or_else()` เป็นเมธอดที่ใช้กับ Result หรือ Option ใน Rust ซึ่งมีความยืดหยุ่นมากกว่า `unwrap_or()`
> ```rust
> result.unwrap_or_else(|err| { /* คำสั่งจัดการกับ error */ })
> option.unwrap_or_else(|| { /* คำสั่งสร้างค่าทดแทน */ })
> ```

## โจทย์:

##### ⭐️

1. เติมโค้ดให้สมบูรณ์เพื่อจัดการกับ Result จากการแปลงสตริงเป็นตัวเลข

```rust, editable
fn main() {
    let number_str = "10";
    let parsed_number = number_str.parse::<i32>();

    match ___ {
        Ok(num) => println!("ตัวเลขที่แปลงได้: {}", ___),
        Err(_) => println!("___"),
    }
}
```

2. เติมโค้ดให้สมบูรณ์เพื่อจัดการกับ Option ที่ได้จากการหาค่าสูงสุดในเวกเตอร์

```rust, editable
fn main() {
    let numbers = vec![1, 5, 3, 2, 4];
    let max_number = numbers.___;

    match ___ {
        Some(max) => println!("ค่าสูงสุดคือ: {}", ___),
        None => println!("___"),
    }
}
```

##### ⭐️⭐️

1. เติมโค้ดให้สมบูรณ์เพื่อจัดการกับ Result จากการอ่าน environment variable โดยใช้ ?
   operator

```rust, editable
use std::env;
use std::error::Error;

fn get_api_key() -> Result<String, Box<dyn Error>> {
    let api_key = env::var("___")?;
    if api_key.___(10) {
        Ok(___)
    } else {
        Err("API key ต้องมีความยาวอย่างน้อย 10 ตัวอักษร".into())
    }
}

fn main() {
    match get_api_key() {
        Ok(key) => println!("API key: {}", key),
        Err(e) => println!("เกิดข้อผิดพลาด: {}", e),
    }
}
```

2. เติมโค้ดให้สมบูรณ์เพื่อจัดการกับ Option โดยใช้ and_then() method

```rust, editable
fn double(x: i32) -> Option<i32> {
    Some(x * 2)
}

fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    let first_doubled = numbers.first()
        .___(___)
        .___(___ * 2);

    match first_doubled {
        Some(n) => println!("ผลลัพธ์: {}", n),
        None => println!("ไม่สามารถคำนวณได้"),
    }
}
```

##### ⭐️⭐️⭐️

1. เติมโค้ดให้สมบูรณ์เพื่อสร้างฟังก์ชันที่จัดการกับ Result และ Option พร้อมกัน โดยใช้ combinators

```rust, editable
use std::num::ParseIntError;

fn parse_and_double(s: &str) -> Result<Option<i32>, ParseIntError> {
    s.parse::<i32>()
        .___(___ x => {
            if x % 2 == 0 {
                Some(x * 2)
            } else {
                ___
            }
        })
}

fn main() {
    let inputs = vec!["10", "15", "abc", "20"];
    for input in inputs {
        match parse_and_double(input) {
            Ok(Some(n)) => println!("ผลลัพธ์สำหรับ {}: {}", input, n),
            Ok(None) => println!("ไม่สามารถคูณ {} ด้วย 2 ได้", input),
            Err(e) => println!("เกิดข้อผิดพลาดในการแปลง {}: {:?}", input, e),
        }
    }
}
```

2. เติมโค้ดให้สมบูรณ์เพื่อสร้างฟังก์ชันที่จัดการกับข้อผิดพลาดแบบกำหนดเอง (custom error)

```rust, editable
use std::fmt;

#[derive(Debug)]
enum CustomError {
    InvalidInput,
    DivisionByZero,
}

impl fmt::Display for CustomError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        match self {
            CustomError::InvalidInput => write!(f, "ข้อมูลไม่ถูกต้อง"),
            CustomError::DivisionByZero => write!(f, "หารด้วยศูนย์"),
        }
    }
}

fn divide(a: i32, b: i32) -> Result<i32, CustomError> {
    if b == 0 {
        return Err(___);
    }
    if a < 0 || b < 0 {
        return ___;
    }
    Ok(___)
}

fn main() {
    let test_cases = vec![(10, 2), (10, 0), (-5, 2), (8, 4)];
    for (a, b) in test_cases {
        match divide(a, b) {
            Ok(result) => println!("{} / {} = {}", a, b, result),
            Err(e) => println!("เกิดข้อผิดพลาด: {}", e),
        }
    }
}
```