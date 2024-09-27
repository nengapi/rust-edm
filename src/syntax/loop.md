# for

> [!NOTE] 
> for ใช้สำหรับการวนซ้ำผ่านชุดข้อมูล เช่น array, vector, หรือ range มักใช้กับ Iterator

ตัวอย่าง:

- แบบเต็ม
```rust, editable
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    for num in numbers.iter() {
        println!("ตัวเลข: {}", num);
    }
}
```

- แบบ shortcut (consume vector)
```rust, editable
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    for num in numbers {
        println!("ตัวเลข: {}", num);
    }
}
```
- แบบใช้กับ iterator
```rust, editable
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    
    for num in &numbers {
        println!("ตัวเลข: {}", num);
    }
}
```

- แบบใช้กับ range
```rust, editable
fn main() {
    for i in 0..5 {
        println!("ลำดับ: {}", i);
    }
}
```

- ใช้กับ range (รวมค่าสุดท้าย)
```rust, editable
fn main() {
    for i in 0..=5 {
        println!("ลำดับ: {}", i);
    }
}
```

# loop

> [!NOTE] 
> loop ใช้สำหรับสร้างการวนซ้ำแบบไม่มีที่สิ้นสุด จนกว่าจะมีคำสั่ง break เพื่อออกจากลูป

ตัวอย่าง:

- แบบไม่มีที่สิ้นสุด
```rust, editable
fn main() {
    let mut counter = 0;
    loop {
        println!("นับ: {}", counter);
        counter += 1;
        if counter == 5 {
            break;
        }
    }

    
}
```

- แบบส่งค่ากลับ
```rust, editable
fn main() {
    let result = loop {
        counter += 1;
        if counter == 10 {
            break counter * 2;
        }
    };
    println!("ผลลัพธ์: {}", result);
}
```

# break

> [!NOTE] 
> break ใช้เพื่อออกจากลูปทันที สามารถใช้ได้กับ while, for และ loop

ตัวอย่าง:

- ใช้ break ใน for loop
```rust, editable
fn main() {
    for i in 1..10 {
        if i == 5 {
            println!("เจอเลข 5 ออกจากลูป!");
            break;
        }
        println!("ตัวเลข: {}", i);
    }
}
```

- ใช้ break ใน loop
```rust, editable
fn main() {
    let mut counter = 0;
    loop {
        println!("นับ: {}", counter);
        counter += 1;
        if counter == 5 {
            break;
        }
    }
}
```

# while

> [!NOTE] 
> เป็นโครงสร้างการวนซ้ำที่ทำงานตราบเท่าที่เงื่อนไขที่กำหนดยังคงเป็นจริง เมื่อเงื่อนไขเป็นเท็จ การวนซ้ำจะหยุดลง

ตัวอย่าง:

```rust, editable
fn main() {
    let mut count = 0;

    while count < 5 {
        println!("นับ: {}", count);
        count += 1;
    }
}
```

# while let

> [!NOTE] 
> while let เป็นรูปแบบพิเศษของ while ที่ใช้สำหรับการจับคู่รูปแบบ (pattern matching) ในขณะที่ทำการวนซ้ำ มักใช้กับ Iterator หรือ Option

ตัวอย่าง:

```rust, editable
fn main() {
    let mut stack = vec![1, 2, 3];

    while let Some(top) = stack.pop() {
        println!("ค่าบนสุดของ stack: {}", top);
    }
}
```

## โจทย์:

##### ⭐️
1. เติมโครงสร้าง for ให้สมบูรณ์เพื่อแสดงผลตัวเลขคู่จาก 1 ถึง 10

```rust, editable
fn main() {
    ___ num in 1..=10 {
        if num % 2 == 0 {
            println!("เลขคู่: {}", num);
        }
    }
}
```

2. เติมโครงสร้าง while ให้สมบูรณ์เพื่อนับเลขจาก 1 ถึง 5

```rust, editable
fn main() {
    let mut count = 1;

    ____ count <= 5 {
        println!("นับ: {}", count);
        count += 1;
    }
}
```

##### ⭐️⭐️
1. เติมโครงสร้าง for และ break ให้สมบูรณ์เพื่อหาตัวเลขที่หารด้วย 7 ลงตัวตัวแรกในช่วง 1 ถึง 100

```rust, editable
fn main() {
    ___ num in 1..=100 {
        if num % 7 == 0 {
            println!("ตัวเลขที่หารด้วย 7 ลงตัวตัวแรกคือ: {}", num);
            ____;
        }
    }
}
```

2. เติมโครงสร้าง while let ให้สมบูรณ์เพื่อแสดงผลค่าใน Vec<Option<i32>> โดยแสดงเฉพาะค่าที่ไม่ใช่ None

```rust, editable
fn main() {
    let numbers = vec![Some(1), None, Some(3), Some(4), None, Some(6)];
    let mut iter = numbers.into_iter();

    ____ let Some(num) = iter.next() {
        println!("ค่าที่ไม่ใช่ None: {}", num);
    }
}
```

##### ⭐️⭐️⭐️
1. เติมโครงสร้าง loop, if, else if, break และ continue ให้สมบูรณ์เพื่อสร้างฟังก์ชันหาจำนวนเฉพาะ n ตัวแรก พร้อมทั้งคำนวณผลรวมของจำนวนเฉพาะเหล่านั้น

```rust, editable
fn find_primes_and_sum(n: u32) -> (Vec<u32>, u32) {
    let mut primes = Vec::new();
    let mut sum = 0;
    let mut num = 2;

    ____ primes.len() < n as usize {
        let mut is_prime = true;

        ____ i in 2..num {
            ____ num % i == 0 {
                is_prime = false;
                ____;
            }
            ____ i * i > num {
                ____;
            }
        }

        ____ is_prime {
            primes.push(num);
            sum += num;
        }

        num += 1;
    }

    (primes, sum)
}

fn main() {
    let (primes, sum) = find_primes_and_sum(10);
    assert_eq!(primes, vec![2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
    assert_eq!(sum, 129);
    println!("First 10 primes: {:?}", primes);
    println!("Sum of first 10 primes: {}", sum);
}
```


2. เติมโครงสร้าง loop, if, else, break และ continue ให้สมบูรณ์เพื่อสร้างฟังก์ชันหาค่า Collatz sequence ที่ยาวที่สุดสำหรับจำนวนตั้งต้นไม่เกิน n

```rust, editable
fn longest_collatz_sequence(n: u64) -> (u64, u64) {
    let mut longest_length = 0;
    let mut starting_number = 0;

    ____ start in 1..=n {
        let mut length = 1;
        let mut num = start;

        ____ {
            ____ num == 1 {
                ____;
            }

            ____ num % 2 == 0 {
                num /= 2;
            } ____ {
                num = 3 * num + 1;
            }

            length += 1;

            ____ num > n && length > longest_length {
                ____;
            }
        }

        ____ length > longest_length {
            longest_length = length;
            starting_number = start;
        }
    }

    (starting_number, longest_length)
}

fn main() {
    let (number, length) = longest_collatz_sequence(1_000_000);
    assert_eq!(number, 837799);
    assert_eq!(length, 525);
    println!("Number {} has the longest Collatz sequence of length {}", number, length);
}
```