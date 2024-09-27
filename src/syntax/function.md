# Function

> [!NOTE] 
> Function คือบล็อกของโค้ดที่ทำงานเฉพาะอย่าง สามารถรับพารามิเตอร์และส่งค่ากลับได้ ใน Rust เราใช้คีย์เวิร์ด `fn` เพื่อประกาศฟังก์ชัน

ตัวอย่าง:

```rust, editable
fn greet(name: &str) {
    println!("สวัสดี, {}!", name);
}

fn main() {
    greet("คุณผู้ใช้");
}
```

ตัวอย่าง:

```rust, editable
fn add(left: i32, right: i32) -> i32 { left + right }
fn sub(left: i32, right: i32) -> i32 { left - right }

fn select(name: &str) -> fn(i32, i32) -> i32 {
    match name {
        "add" => add,
        "sub" => sub,
        _ => panic!("Unknown function"),
    }
}

fn main() {
    let fun = select("add");
    println!("{} + {} = {}", 1, 2, fun(1, 2));
}
```

## โจทย์:

##### ⭐️
1. เติม function signature ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่รับชื่อและอายุ แล้วพิมพ์ข้อความทักทาย

```rust, editable
___ greet(name: ___, age: ___) {
    println!("สวัสดี {} คุณอายุ {} ปี", name, age);
}

fn main() {
    greet("อลิซ", 25);
}
```

2. เติม function signature ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่คำนวณพื้นที่สี่เหลี่ยมผืนผ้า

```rust, editable
___ calculate_rectangle_area(width: ___, height: ___) ___ {
    width * height
}

fn main() {
    let area = calculate_rectangle_area(5.0, 3.0);
    println!("พื้นที่สี่เหลี่ยมผืนผ้า: {}", area);
}
```

##### ⭐️⭐️
1. เติม function signature และ implementation ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่ตรวจสอบว่าตัวเลขเป็นจำนวนเฉพาะหรือไม่

```rust, editable
___ is_prime(n: u32) ___ {
    if n <= 1 {
        return false;
    }
    for i in 2..=(n as f64).sqrt() as u32 {
        if n % i == 0 {
            return ___;
        }
    }
    ___
}

fn main() {
    println!("17 เป็นจำนวนเฉพาะ: {}", is_prime(17));
    println!("4 เป็นจำนวนเฉพาะ: {}", is_prime(4));
}
```

2. เติม function signature และ implementation ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่หาค่า factorial ของตัวเลข

```rust, editable
___ factorial(n: u32) ___ {
    if n == 0 || n == 1 {
        ___
    } else {
        n * factorial(___)
    }
}

fn main() {
    println!("5! = {}", factorial(5));
}
```

##### ⭐️⭐️⭐️
1. เติม function signature และ implementation ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่หาจำนวน Fibonacci ลำดับที่ n โดยใช้ memoization

```rust, editable
use std::collections::HashMap;

fn fibonacci(n: u32, memo: &mut HashMap<u32, u64>) -> u64 {
    if let Some(&result) = memo.get(&n) {
        return result;
    }

    let result = if n <= 1 {
        ___
    } else {
        fibonacci(___, memo) + fibonacci(___, memo)
    };

    memo.insert(n, result);
    result
}

fn main() {
    let mut memo = HashMap::new();
    println!("Fibonacci(10) = {}", fibonacci(10, &mut memo));
}
```

2. เติม function signature และ implementation ให้สมบูรณ์เพื่อสร้างฟังก์ชันที่หาค่า Greatest Common Divisor (GCD) ของสองจำนวนโดยใช้ Euclidean algorithm

```rust, editable
___ gcd(mut a: u64, mut b: u64) ___ {
    while b != 0 {
        let temp = ___;
        b = ___;
        a = ___;
    }
    ___
}

fn main() {
    println!("GCD ของ 48 และ 18 คือ: {}", gcd(48, 18));
}
```