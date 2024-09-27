# Asynchronous Runtime

> [!NOTE]
>
> - โดยปกติแล้ว การทำงานของ Rust จะเป็น Synchronous หมายความว่า
>   ทุกอย่างจะต้องทำงานอย่างต่อเนื่องจากการทำงานของตัวมันเอง
> - แต่ถ้าหากต้องการทำงานแบบ Parallel หรือ Asynchronous, Rust
>   เองก็มีการสนับสนุนในการทำงานแบบนั้นได้ โดยการใช้งาน Thread หรือ Task หรือ Future
>   (คล้ายๆ Promise ใน NodeJS) ด้วยเช่นกัน
> - แต่ก็มีทางเลือกอีกทางที่ง่ายกว่านั้น ก็คือการใช้งาน Async Runtime ผ่าน Crate ที่ชื่อว่า `Tokio`
> - `Tokio` คือ Crate ที่สร้างขึ้นมาเพื่อสนับสนุนการทำงานแบบ Asynchronous และ Parallel ใน
>   Rust โดยทำหน้าที่จัดการการทำงานของ Thread หรือ Task หรือ Future ให้ง่ายขึ้น ผ่าน Syntax
>   `Async/Await` ที่เราคุ้นเคยกันมาจาก NodeJS
> - Web framework หรือ Database ส่วนใหญ่ของ Rust จะทำงานแบบ Asynchronous อยู่บน
>   `Tokio Runtime` เช่น `Axum`, `Actix`, `Rocket`, `Warp`

> [!TIP]
>
> - `Async/Await` ของ `Tokio Rust` จะใช้งานคล้ายกับ `Async/Await` ของ NodeJS
>   แต่เบื้องหลังการทำงานจะแตกต่างกัน
>   - สำหรับ NodeJS จะใช้งานผ่าน `Event Loop` ที่ทำงานอยู่ในภายใน Single Thread
>   - สำหรับ Rust จะใช้งานผ่าน `Thread` หรือ `Task` ที่ทำงานอยู่ในภายใน `Thread Pool`
>     ซึ่งจะทำงานอยู่บน Core ของ CPU ที่มีทั้งหมด ทำให้ Rust สามารถทำงานแบบ Parallel
>     ได้โดยสมบูรณ์

## How Tokio Runtime Work

> [!TIP]
>
> - **Thread Pool**: `Tokio` ใช้ thread pool ในการจัดการ task ต่างๆ โดยจะมีการสร้าง
>   thread ขึ้นมาเป็นจำนวนหนึ่งตามจำนวน core ของ CPU ที่มีอยู่
> - **Task Scheduling**: `Tokio` มี task scheduler ที่ทำหน้าที่จัดสรร task ต่างๆ ให้กับ
>   thread pool เพื่อให้การทำงานเป็นไปอย่างมีประสิทธิภาพ
> - **Async/Await**: การใช้งาน `async` และ `await` ใน `Tokio`
>   จะช่วยให้การเขียนโค้ดแบบ asynchronous ง่ายขึ้น โดยไม่ต้องจัดการกับ thread โดยตรง
> - **Event Loop**: `Tokio` มี event loop ที่ทำหน้าที่ตรวจสอบ event ต่างๆ และจัดการกับ
>   task ที่พร้อมจะทำงาน
> - **Resource Management**: `Tokio` จัดการ resource ต่างๆ เช่น network connection,
>   file I/O, และ timer ให้เป็นไปอย่างมีประสิทธิภาพ
> - **Thread Safety**: `Tokio` จัดการ thread ให้เป็นไปอย่างปลอดภัยในการเข้าถึง resource
>   ต่างๆ โดยใช้ `Send` และ `Sync` trait ของ Rust เพื่อให้แน่ใจว่า data ที่ถูกแชร์ระหว่าง
>   thread นั้นปลอดภัย

## How to use Tokio Runtime

### Add Dependency

```toml
[dependencies]
tokio = { version = "1.0", features = ["macro", "rt-multi-thread"] }
```

or

```sh
cargo add tokio -F rt-multi-thread,macro
```

### Change Main Function to `#[tokio::main]`

```rust
#[tokio::main]
async fn main() {
    println!("Hello, world!");
}
```

### Use Async/Await Function

```rust
// Define `async` keyword in front of function
async fn do_something() {
    // TODO: Implement
}

#[tokio::main]
async fn main() {
    // use .await to run async function
    do_something().await;
}
```
