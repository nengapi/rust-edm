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
1. เติมโครงสร้าง while let ให้สมบูรณ์เพื่อแสดงผลค่าใน Vec<Option<i32>> โดยแสดงเฉพาะค่าที่ไม่ใช่ None

```rust, editable
fn main() {
    let numbers = vec![Some(1), None, Some(3), Some(4), None, Some(6)];
    let mut iter = numbers.into_iter();

    ______ = iter.next() {
        println!("ค่าที่ไม่ใช่ None: {}", num);
    }
}
```
