# 📘 Java OOP -- Cẩm nang học nhanh & thực hành

> Tài liệu tổng hợp **Object-Oriented Programming (OOP) trong Java**,
> phát triển từ bộ ghi chú OOP được cung cấp và mở rộng theo hướng học
> để áp dụng thực tế.
>
> Mục tiêu: **Hiểu bản chất → đọc code → tự viết code → áp dụng vào
> project Java/Spring Boot.**

------------------------------------------------------------------------

## 📑 Mục lục

1.  [OOP là gì?](#1-oop-là-gì)
2.  [Class](#2-class)
3.  [Object](#3-object)
4.  [Method](#4-method)
5.  [Constructor](#5-constructor)
6.  [Inheritance](#6-inheritance--kế-thừa)
7.  [Polymorphism](#7-polymorphism--đa-hình)
8.  [Encapsulation](#8-encapsulation--đóng-gói)
9.  [Abstraction](#9-abstraction--trừu-tượng)
10. [4 tính chất quan trọng của OOP](#10-4-tính-chất-quan-trọng-của-oop)
11. [OOP trong project thực tế](#11-oop-trong-project-thực-tế)
12. [Lỗi thường gặp](#12-lỗi-thường-gặp)
13. [Cheat Sheet](#13-cheat-sheet)
14. [Bài tập thực hành](#14-bài-tập-thực-hành)
15. [Lời giải & giải thích](#15-lời-giải--giải-thích)

------------------------------------------------------------------------

# 1. OOP là gì?

**OOP -- Object-Oriented Programming** (Lập trình hướng đối tượng) là
cách tổ chức chương trình xoay quanh các **object**.

Một object thường gồm:

-   **State / Data**: trạng thái, dữ liệu.
-   **Behavior**: hành vi mà object có thể thực hiện.

Ví dụ một `Car`:

``` text
Car
├── Data
│   ├── brand
│   ├── color
│   └── speed
│
└── Behavior
    ├── start()
    ├── accelerate()
    └── stop()
```

Trong Java:

``` java
class Car {
    String brand;
    String color;
    int speed;

    void start() {
        System.out.println("Car started");
    }

    void stop() {
        System.out.println("Car stopped");
    }
}
```

### Vì sao dùng OOP?

OOP giúp:

-   chia chương trình thành các thành phần dễ quản lý;
-   tái sử dụng code;
-   bảo vệ dữ liệu;
-   giảm phụ thuộc giữa các thành phần;
-   dễ mở rộng và bảo trì;
-   mô hình hóa các đối tượng/nghiệp vụ thực tế.

> Cách nhớ: **Class thiết kế → Object được tạo → Object giữ dữ liệu →
> Method xử lý hành vi.**

------------------------------------------------------------------------

# 2. Class

## 2.1 Class là gì?

**Class là khuôn mẫu (blueprint) dùng để tạo object.**

Ví dụ:

``` java
class Student {
    int id;
    String name;
    double marks;

    void display() {
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Marks: " + marks);
    }
}
```

`Student` mô tả rằng một sinh viên có:

``` text
Student
├── Attributes
│   ├── id
│   ├── name
│   └── marks
│
└── Methods
    └── display()
```

## 2.2 Cú pháp

``` java
class ClassName {

    // attributes
    DataType attribute;

    // methods
    ReturnType methodName() {
        // logic
    }
}
```

## 2.3 Class và bộ nhớ

Nói đơn giản, khai báo class mới chỉ tạo ra **định nghĩa kiểu/khuôn
mẫu**. Dữ liệu instance của từng object được cấp phát khi object được
tạo.

``` java
class Student {
    int id;
}
```

Chưa có `Student` cụ thể.

``` java
Student student = new Student();
```

Bây giờ một instance đã được tạo.

> Lưu ý: JVM còn phải lưu metadata của class, vì vậy không nên hiểu
> tuyệt đối rằng "class không chiếm bất kỳ bộ nhớ nào". Điều cần nhớ ở
> mức OOP là **khai báo class không đồng nghĩa tạo instance**.

------------------------------------------------------------------------

# 3. Object

## 3.1 Object là gì?

Object là **instance (thể hiện)** được tạo từ một class.

``` java
Student s1 = new Student();
Student s2 = new Student();
```

Cả `s1` và `s2` đều dựa trên `Student`, nhưng là hai object khác nhau.

``` java
s1.id = 101;
s1.name = "An";

s2.id = 102;
s2.name = "Linh";
```

Mô hình:

``` text
                    Student Class
                  /               \
                 /                 \
        Student object          Student object
             s1                     s2
        id = 101                id = 102
        name = An               name = Linh
```

## 3.2 Dòng này thực sự có gì?

``` java
Student s1 = new Student();
```

Có thể đọc:

``` text
Student     s1        =       new Student();
   │         │                    │
kiểu      biến tham chiếu      tạo object
```

`s1` là **reference variable** tham chiếu tới object `Student`.

## 3.3 Nhiều reference có thể trỏ cùng object

``` java
Student s1 = new Student();
Student s2 = s1;

s1.name = "An";

System.out.println(s2.name);
```

Kết quả:

``` text
An
```

Vì:

``` text
s1 ─────┐
        ├────> Student Object
s2 ─────┘       name = "An"
```

Đây là điểm rất quan trọng khi làm Java thực tế.

------------------------------------------------------------------------

# 4. Method

## 4.1 Method là gì?

Method là một khối code thuộc class, dùng để thực hiện một nhiệm vụ.

``` java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    void showMessage() {
        System.out.println("Hello Java");
    }
}
```

## 4.2 Cấu trúc method

``` java
accessModifier returnType methodName(parameters) {
    // logic
    return value;
}
```

Ví dụ:

``` java
public int add(int a, int b) {
    return a + b;
}
```

  Thành phần        Giá trị
  ----------------- ----------------
  Access modifier   `public`
  Return type       `int`
  Method name       `add`
  Parameters        `int a, int b`
  Return            `a + b`

## 4.3 Method có return

``` java
int result = calculator.add(10, 20);
```

Luồng:

``` text
10, 20
   ↓
 add()
   ↓
10 + 20
   ↓
  30
```

## 4.4 Method `void`

Nếu method không trả về giá trị:

``` java
void hello() {
    System.out.println("Hello");
}
```

Gọi:

``` java
hello();
```

## 4.5 Parameter và Argument

``` java
void hello(String name) {
}
```

`name` là **parameter**.

``` java
hello("An");
```

`"An"` là **argument**.

------------------------------------------------------------------------

# 5. Constructor

## 5.1 Constructor là gì?

Constructor là thành phần đặc biệt dùng để **khởi tạo object**.

``` java
class Student {

    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

Tạo object:

``` java
Student student = new Student(101, "An");
```

Luồng:

``` text
new Student(101, "An")
          ↓
Student(int id, String name)
          ↓
gán dữ liệu ban đầu
          ↓
Student object
```

## 5.2 Quy tắc

Constructor:

-   có tên giống class;
-   không khai báo kiểu trả về;
-   được chạy khi tạo object bằng constructor đó;
-   có thể nhận parameter;
-   có thể overload.

Sai:

``` java
void Student() {
}
```

Đây là **method**, không phải constructor.

Đúng:

``` java
Student() {
}
```

## 5.3 Default constructor

Nếu bạn **không khai báo constructor nào**, compiler có thể cung cấp
constructor không tham số mặc định:

``` java
class Student {
}
```

Có thể:

``` java
Student s = new Student();
```

Nhưng khi bạn tự khai báo:

``` java
class Student {

    Student(String name) {
    }
}
```

thì Java không tự thêm `Student()` cho bạn.

Dòng sau sẽ lỗi:

``` java
Student s = new Student();
```

Muốn dùng cả hai:

``` java
class Student {

    Student() {
    }

    Student(String name) {
    }
}
```

## 5.4 `this`

``` java
class Student {

    private String name;

    Student(String name) {
        this.name = name;
    }
}
```

Trong đó:

``` text
this.name = name
    │        │
 field    parameter
```

`this` đại diện cho **object hiện tại**.

## 5.5 Constructor overloading

``` java
class Student {

    String name;
    int age;

    Student() {
    }

    Student(String name) {
        this.name = name;
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

------------------------------------------------------------------------

# 6. Inheritance -- Kế thừa

## 6.1 Inheritance là gì?

Inheritance cho phép một class kế thừa các thành phần có thể truy cập
được từ class khác.

``` java
class Animal {

    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Barking...");
    }
}
```

Sử dụng:

``` java
Dog dog = new Dog();

dog.eat();
dog.bark();
```

Mô hình:

``` text
       Animal
          │
       extends
          │
          ▼
         Dog
```

Quan hệ:

``` text
Dog IS-A Animal
```

## 6.2 Superclass và Subclass

``` java
class Animal {
}
```

`Animal` = superclass / parent class.

``` java
class Dog extends Animal {
}
```

`Dog` = subclass / child class.

## 6.3 `super`

``` java
class Animal {

    String name;

    Animal(String name) {
        this.name = name;
    }
}

class Dog extends Animal {

    Dog(String name) {
        super(name);
    }
}
```

`super(...)` gọi constructor của class cha.

## 6.4 Điều cần nhớ

-   Java class chỉ `extends` trực tiếp một class.
-   Constructor không được kế thừa.
-   Thành viên `private` của cha vẫn là một phần trạng thái của object
    cha/con nhưng subclass **không truy cập trực tiếp** bằng tên field
    đó.
-   Có thể dùng `protected`, `public` hoặc API của superclass tùy thiết
    kế.
-   Interface giúp Java hỗ trợ nhiều kiểu/contract.

------------------------------------------------------------------------

# 7. Polymorphism -- Đa hình

Polymorphism nghĩa là **một interface/type chung có thể biểu diễn nhiều
implementation/hình thái khác nhau**.

Hai khái niệm thường học:

``` text
Polymorphism
├── Compile-time → Overloading
└── Runtime      → Overriding / Dynamic Dispatch
```

------------------------------------------------------------------------

## 7.1 Method Overloading

Cùng tên method nhưng **danh sách parameter khác nhau**.

``` java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

Gọi:

``` java
calculator.add(10, 20);
calculator.add(10, 20, 30);
calculator.add(10.5, 20.5);
```

Compiler lựa chọn overload phù hợp dựa trên chữ ký/lập luận truyền vào.

### Không thể overload chỉ bằng return type

Sai:

``` java
int getValue() {
    return 1;
}

double getValue() {
    return 1.0;
}
```

------------------------------------------------------------------------

## 7.2 Method Overriding

Class con cung cấp implementation mới cho instance method có thể
override từ class cha.

``` java
class Animal {

    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

Điểm quan trọng:

``` java
Animal animal = new Dog();
animal.sound();
```

Kết quả:

``` text
Dog barks
```

Tại sao?

``` text
Reference type          Actual object
    Animal      ───────>    Dog
                              │
                              ▼
                         Dog.sound()
```

Với instance method được override, JVM dispatch theo **object thực tế**
tại runtime.

## 7.3 Overloading vs Overriding

  Tiêu chí              Overloading      Overriding
  --------------------- ---------------- --------------------------
  Method name           Giống            Giống
  Parameter list        Phải khác        Giống
  Quan hệ kế thừa       Không bắt buộc   Có
  Chọn implementation   Compile time     Runtime với override
  Mục tiêu              Nhiều cách gọi   Thay đổi hành vi kế thừa

> Nên dùng `@Override` khi override để compiler giúp phát hiện lỗi.

------------------------------------------------------------------------

# 8. Encapsulation -- Đóng gói

## 8.1 Encapsulation là gì?

Encapsulation gom dữ liệu và hành vi liên quan vào object/class và
**kiểm soát cách bên ngoài truy cập trạng thái**.

Ví dụ:

``` java
class BankAccount {

    private double balance;

    public double getBalance() {
        return balance;
    }
}
```

Bên ngoài không thể:

``` java
account.balance = 1000000;
```

nếu `balance` là `private`.

## 8.2 Getter / Setter

``` java
class Student {

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Sử dụng:

``` java
Student student = new Student();

student.setName("An");

System.out.println(student.getName());
```

## 8.3 Setter không chỉ để gán

Encapsulation có giá trị nhất khi object **bảo vệ invariant/quy tắc
nghiệp vụ**.

``` java
class BankAccount {

    private double balance;

    public void deposit(double amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException(
                "Amount must be greater than 0"
            );
        }

        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

Bây giờ object tự bảo vệ dữ liệu:

``` text
Client
  │
  │ deposit(100)
  ▼
BankAccount
  │
  ├── validate
  ├── update balance
  │
  ▼
Valid state
```

Thay vì cho phép:

``` java
account.setBalance(-999999);
```

Trong thiết kế thực tế, **không phải field nào cũng cần setter**.

## 8.4 Access modifiers

  -----------------------------------------------------------------------------
  Modifier              Same class   Same package  Subclass khác        Mọi nơi
                                                         package 
  ----------------- -------------- -------------- -------------- --------------
  `private`                     ✅             ❌             ❌             ❌

  package-private               ✅             ✅             ❌             ❌

  `protected`                   ✅             ✅           ✅\*             ❌

  `public`                      ✅             ✅             ✅             ✅
  -----------------------------------------------------------------------------

`protected` ở subclass khác package có các quy tắc truy cập chi tiết
hơn; bảng trên chỉ dùng để ghi nhớ mức cơ bản.

------------------------------------------------------------------------

# 9. Abstraction -- Trừu tượng

Bộ ảnh thiếu trang Abstraction, nhưng đây là một trong bốn trụ cột OOP
nên cần bổ sung.

## 9.1 Abstraction là gì?

Abstraction tập trung vào:

> **Object làm được gì?**

thay vì bắt code sử dụng object phải biết:

> **Bên trong nó làm như thế nào?**

Ví dụ:

``` java
paymentService.pay();
```

Code gọi không cần biết chi tiết:

``` text
Validate
   ↓
Create transaction
   ↓
Call payment gateway
   ↓
Save transaction
   ↓
Return result
```

------------------------------------------------------------------------

## 9.2 Abstract class

``` java
abstract class Animal {

    abstract void sound();

    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

Class con:

``` java
class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Woof");
    }
}
```

Không thể:

``` java
new Animal();
```

nếu `Animal` là abstract class.

------------------------------------------------------------------------

## 9.3 Interface

``` java
interface PaymentService {

    void pay(double amount);
}
```

Implementation:

``` java
class MomoPaymentService implements PaymentService {

    @Override
    public void pay(double amount) {
        System.out.println("Pay with Momo: " + amount);
    }
}
```

Implementation khác:

``` java
class BankPaymentService implements PaymentService {

    @Override
    public void pay(double amount) {
        System.out.println("Pay with bank: " + amount);
    }
}
```

Client:

``` java
PaymentService service =
        new MomoPaymentService();

service.pay(500000);
```

Đổi implementation:

``` java
PaymentService service =
        new BankPaymentService();
```

Client vẫn làm việc thông qua contract `PaymentService`.

## 9.4 Abstract class vs Interface

  -----------------------------------------------------------------------
  Abstract class                      Interface
  ----------------------------------- -----------------------------------
  Có thể giữ instance state           Chủ yếu định nghĩa contract; field
                                      khai báo trong interface là
                                      constants

  Có constructor                      Không có constructor instance

  Class dùng `extends`                Class dùng `implements`

  Một class chỉ extends một class     Một class có thể implements nhiều
                                      interface

  Có abstract + concrete methods      Có abstract methods và có thể có
                                      `default`, `static`, `private`
                                      methods
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 10. 4 tính chất quan trọng của OOP

``` text
                    OOP
                     │
       ┌─────────────┼─────────────┐
       │             │             │
Encapsulation   Inheritance   Polymorphism
       │             │             │
       └─────────────┼─────────────┘
                     │
                Abstraction
```

## Encapsulation

``` text
Ẩn/kiểm soát state
        ↓
Expose API phù hợp
        ↓
Bảo vệ object
```

## Inheritance

``` text
Animal
  │
  ├── Dog
  └── Cat
```

Tái sử dụng/mở rộng hành vi trong quan hệ **IS-A** phù hợp.

## Polymorphism

``` text
Animal animal = new Dog();

animal.sound();
        ↓
    Dog.sound()
```

## Abstraction

``` text
PaymentService
      │
 ┌────┴────┐
 │         │
Momo      Bank
```

Code phụ thuộc vào abstraction thay vì implementation cụ thể.

------------------------------------------------------------------------

# 11. OOP trong project thực tế

Ví dụ cấu trúc thường gặp trong Spring Boot:

``` text
Controller
    │
    ▼
Service Interface
    │
    ▼
Service Implementation
    │
    ▼
Repository
    │
    ▼
Database
```

Ví dụ:

``` java
public interface UserService {

    User getUser(Long id);
}
```

Implementation:

``` java
@Service
public class UserServiceImpl implements UserService {

    private final UserRepository userRepository;

    public UserServiceImpl(
            UserRepository userRepository
    ) {
        this.userRepository = userRepository;
    }

    @Override
    public User getUser(Long id) {
        return userRepository
                .findById(id)
                .orElseThrow();
    }
}
```

Controller phụ thuộc vào abstraction:

``` java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(
            UserService userService
    ) {
        this.userService = userService;
    }
}
```

Ở đây bạn có thể thấy:

-   `UserController`, `UserServiceImpl` → **Class**
-   object Spring tạo từ các class → **Object**
-   `getUser()` → **Method**
-   constructor injection → **Constructor**
-   field `private final` → hỗ trợ **Encapsulation**
-   `implements UserService` → **Abstraction**
-   biến kiểu `UserService` có thể nhận implementation phù hợp →
    **Polymorphism**

> Lưu ý: Spring thường ưu tiên **composition + dependency injection**
> hơn việc lạm dụng inheritance.

------------------------------------------------------------------------

# 12. Lỗi thường gặp

## 12.1 Nhầm Class và Object

Sai cách nghĩ:

``` text
Student = object
```

Đúng:

``` text
Student = class

new Student() = object
```

------------------------------------------------------------------------

## 12.2 Constructor có `void`

Sai:

``` java
void Student() {
}
```

Đúng:

``` java
Student() {
}
```

------------------------------------------------------------------------

## 12.3 Field để `public` hết

Không nên:

``` java
class User {

    public String email;
    public String password;
}
```

Thường nên kiểm soát state:

``` java
class User {

    private String email;
    private String password;
}
```

Nhưng cũng không nên máy móc tạo setter cho mọi field.

------------------------------------------------------------------------

## 12.4 Nhầm Overload và Override

``` java
add(int, int)
add(int, int, int)
```

→ Overloading.

``` java
class Animal {
    void sound() {}
}

class Dog extends Animal {
    @Override
    void sound() {}
}
```

→ Overriding.

------------------------------------------------------------------------

## 12.5 Nghĩ `private` được subclass truy cập trực tiếp

``` java
class Animal {
    private String name;
}

class Dog extends Animal {

    void print() {
        // System.out.println(name); // lỗi
    }
}
```

Hãy expose hành vi/API phù hợp hoặc cân nhắc access modifier theo thiết
kế.

------------------------------------------------------------------------

## 12.6 Lạm dụng inheritance

Không phải cứ muốn tái sử dụng code là:

``` java
class A extends B
```

Hãy hỏi:

``` text
A có thực sự IS-A B không?
```

Ví dụ:

``` text
Dog IS-A Animal       ✅
Car IS-A Engine       ❌
Car HAS-A Engine      ✅
```

Trường hợp sau phù hợp với **composition**:

``` java
class Car {

    private Engine engine;
}
```

------------------------------------------------------------------------

# 13. Cheat Sheet

  -----------------------------------------------------------------------
  Khái niệm                           Câu hỏi cần nhớ
  ----------------------------------- -----------------------------------
  Class                               Object được thiết kế như thế nào?

  Object                              Instance cụ thể nào đang tồn tại?

  Attribute                           Object giữ dữ liệu gì?

  Method                              Object làm được gì?

  Constructor                         Object được khởi tạo thế nào?

  Encapsulation                       Ai được phép thay đổi state?

  Inheritance                         Class này có quan hệ IS-A với class
                                      kia không?

  Polymorphism                        Một type chung có thể chạy nhiều
                                      implementation không?

  Abstraction                         Client cần biết contract nào, và có
                                      thể bỏ qua chi tiết nào?

  Interface                           Contract giữa các thành phần là gì?

  `this`                              Object hiện tại

  `super`                             Thành phần/class cha

  `extends`                           Kế thừa class

  `implements`                        Thực thi interface

  `@Override`                         Ghi đè method
  -----------------------------------------------------------------------

### Sơ đồ tổng hợp

``` text
                    CLASS
                      │
                   new │
                      ▼
                   OBJECT
                 /        \
              data       behavior
               │             │
        Encapsulation      Method
                             │
              ┌──────────────┴──────────────┐
              │                             │
         Inheritance                   Abstraction
              │                             │
              └────────── Polymorphism ─────┘
```

------------------------------------------------------------------------

# 14. Bài tập thực hành

> **Quan trọng:** Hãy tự làm phần này trước khi đọc lời giải bên dưới.

------------------------------------------------------------------------

## Bài 1 -- Student Management

### Yêu cầu

Tạo class:

``` text
Student
```

có:

``` text
id
name
score
```

Yêu cầu:

1.  Các field phải `private`.
2.  Tạo constructor.
3.  Tạo getter cần thiết.
4.  `score` chỉ được nằm trong `0 → 10`.
5.  Tạo method:

``` java
displayInfo()
```

6.  Tạo:

``` java
isPassed()
```

Nếu:

``` text
score >= 5
```

trả về `true`.

### Kiến thức sử dụng

-   Class
-   Object
-   Constructor
-   Method
-   Encapsulation

------------------------------------------------------------------------

## Bài 2 -- Bank Account

Tạo:

``` text
BankAccount
```

có:

``` text
accountNumber
ownerName
balance
```

Method:

``` java
deposit(double amount)
withdraw(double amount)
getBalance()
```

Quy tắc:

``` text
deposit <= 0
→ không hợp lệ

withdraw <= 0
→ không hợp lệ

withdraw > balance
→ không cho rút
```

Không được tạo:

``` java
setBalance()
```

### Câu hỏi

Tại sao không nên có `setBalance()`?

------------------------------------------------------------------------

## Bài 3 -- Animal

Tạo:

``` text
Animal
  │
  ├── Dog
  └── Cat
```

`Animal` có:

``` java
sound()
```

`Dog`:

``` text
Woof
```

`Cat`:

``` text
Meow
```

Sau đó:

``` java
Animal a1 = new Dog();
Animal a2 = new Cat();

a1.sound();
a2.sound();
```

### Hãy giải thích

Tại sao biến có kiểu `Animal` nhưng lại chạy `Dog.sound()` /
`Cat.sound()`?

------------------------------------------------------------------------

## Bài 4 -- Payment System

Thiết kế:

``` text
PaymentService
       │
       ├── MomoPayment
       │
       └── BankPayment
```

Interface:

``` java
void pay(double amount);
```

Tạo class:

``` text
CheckoutService
```

nhận `PaymentService` thông qua constructor.

Yêu cầu:

``` java
CheckoutService checkout =
    new CheckoutService(
        new MomoPayment()
    );

checkout.checkout(500000);
```

Sau đó đổi sang:

``` java
new BankPayment()
```

mà không sửa logic `checkout()`.

### Kiến thức

-   Interface
-   Abstraction
-   Polymorphism
-   Constructor injection
-   Composition

------------------------------------------------------------------------

## Bài 5 -- Mini Order System ⭐

Thiết kế:

``` text
Product
Customer
OrderItem
Order
PaymentService
```

### Product

``` text
id
name
price
```

### Customer

``` text
id
name
email
```

### OrderItem

``` text
product
quantity
```

Có method:

``` java
getSubtotal()
```

### Order

``` text
customer
items
```

Có:

``` java
addItem()
getTotal()
displayOrder()
```

### Payment

``` text
PaymentService
       │
       ├── CashPayment
       └── BankPayment
```

Cuối cùng chương trình phải làm được:

``` text
Tạo Customer
      ↓
Tạo Product
      ↓
Tạo Order
      ↓
Add Product
      ↓
Tính Total
      ↓
Payment
      ↓
Hiển thị Order
```

------------------------------------------------------------------------

# 15. Lời giải & giải thích

------------------------------------------------------------------------

## Lời giải Bài 1

``` java
class Student {

    private int id;
    private String name;
    private double score;

    public Student(
            int id,
            String name,
            double score
    ) {
        this.id = id;
        this.name = name;
        setScore(score);
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {

        if (score < 0 || score > 10) {
            throw new IllegalArgumentException(
                "Score must be between 0 and 10"
            );
        }

        this.score = score;
    }

    public boolean isPassed() {
        return score >= 5;
    }

    public void displayInfo() {
        System.out.println(
            id + " - " +
            name + " - " +
            score
        );
    }
}
```

### Giải thích

``` java
private double score;
```

ngăn code bên ngoài thay đổi trực tiếp:

``` java
student.score = 999;
```

Mọi thay đổi đi qua:

``` java
setScore()
```

nên object có thể kiểm tra:

``` text
0 <= score <= 10
```

Đây chính là **Encapsulation**.

Constructor dùng:

``` java
setScore(score);
```

thay vì:

``` java
this.score = score;
```

để ngay cả dữ liệu ban đầu cũng phải qua validation.

------------------------------------------------------------------------

## Lời giải Bài 2

``` java
class BankAccount {

    private String accountNumber;
    private String ownerName;
    private double balance;

    public BankAccount(
            String accountNumber,
            String ownerName
    ) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = 0;
    }

    public void deposit(double amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException(
                "Invalid deposit amount"
            );
        }

        balance += amount;
    }

    public void withdraw(double amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException(
                "Invalid withdrawal amount"
            );
        }

        if (amount > balance) {
            throw new IllegalArgumentException(
                "Insufficient balance"
            );
        }

        balance -= amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

### Tại sao không có `setBalance()`?

Nếu có:

``` java
account.setBalance(-1000000);
```

client có thể phá vỡ quy tắc nghiệp vụ.

Thay vào đó:

``` text
balance
   ↑
   │
deposit() / withdraw()
   ↑
   │
 Client
```

Object tự quản lý trạng thái của mình.

Đây là cách hiểu Encapsulation tốt hơn việc chỉ nhớ:

> "`private` + getter/setter".

------------------------------------------------------------------------

## Lời giải Bài 3

``` java
class Animal {

    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Woof");
    }
}

class Cat extends Animal {

    @Override
    void sound() {
        System.out.println("Meow");
    }
}
```

Main:

``` java
public class Main {

    public static void main(String[] args) {

        Animal a1 = new Dog();
        Animal a2 = new Cat();

        a1.sound();
        a2.sound();
    }
}
```

Kết quả:

``` text
Woof
Meow
```

### Giải thích

Xét:

``` java
Animal a1 = new Dog();
```

Có hai khái niệm:

``` text
Animal             Dog
  │                 │
reference type   actual object
```

Khi gọi instance method đã override:

``` java
a1.sound();
```

runtime nhìn object thực tế:

``` text
a1
 │
 ▼
Dog Object
 │
 ▼
Dog.sound()
```

Đây là **runtime polymorphism / dynamic method dispatch**.

------------------------------------------------------------------------

## Lời giải Bài 4

Interface:

``` java
interface PaymentService {

    void pay(double amount);
}
```

Momo:

``` java
class MomoPayment
        implements PaymentService {

    @Override
    public void pay(double amount) {

        System.out.println(
            "Momo payment: " + amount
        );
    }
}
```

Bank:

``` java
class BankPayment
        implements PaymentService {

    @Override
    public void pay(double amount) {

        System.out.println(
            "Bank payment: " + amount
        );
    }
}
```

Checkout:

``` java
class CheckoutService {

    private final PaymentService paymentService;

    public CheckoutService(
            PaymentService paymentService
    ) {
        this.paymentService = paymentService;
    }

    public void checkout(double amount) {

        paymentService.pay(amount);
    }
}
```

Main:

``` java
public class Main {

    public static void main(String[] args) {

        PaymentService payment =
            new MomoPayment();

        CheckoutService checkout =
            new CheckoutService(payment);

        checkout.checkout(500000);
    }
}
```

Đổi:

``` java
PaymentService payment =
    new BankPayment();
```

`CheckoutService` không cần sửa.

### Tại sao đây là thiết kế quan trọng?

Nếu viết:

``` java
private MomoPayment payment;
```

`CheckoutService` phụ thuộc trực tiếp vào Momo.

Nhưng:

``` java
private PaymentService paymentService;
```

thì dependency là abstraction:

``` text
              PaymentService
                    ▲
          ┌─────────┴─────────┐
          │                   │
    MomoPayment          BankPayment
          ▲                   ▲
          └─────────┬─────────┘
                    │
             có thể truyền vào
                    │
            CheckoutService
```

Đây là tư duy xuất hiện rất nhiều trong Spring Boot.

------------------------------------------------------------------------

# Lời giải Bài 5 -- Mini Order System

## Product

``` java
class Product {

    private final long id;
    private final String name;
    private final double price;

    public Product(
            long id,
            String name,
            double price
    ) {

        if (price < 0) {
            throw new IllegalArgumentException(
                "Price cannot be negative"
            );
        }

        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
```

------------------------------------------------------------------------

## Customer

``` java
class Customer {

    private final long id;
    private final String name;
    private final String email;

    public Customer(
            long id,
            String name,
            String email
    ) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }
}
```

------------------------------------------------------------------------

## OrderItem

``` java
class OrderItem {

    private final Product product;
    private final int quantity;

    public OrderItem(
            Product product,
            int quantity
    ) {

        if (quantity <= 0) {
            throw new IllegalArgumentException(
                "Quantity must be greater than 0"
            );
        }

        this.product = product;
        this.quantity = quantity;
    }

    public double getSubtotal() {

        return product.getPrice() * quantity;
    }

    public Product getProduct() {
        return product;
    }

    public int getQuantity() {
        return quantity;
    }
}
```

------------------------------------------------------------------------

## Order

``` java
import java.util.ArrayList;
import java.util.List;

class Order {

    private final Customer customer;

    private final List<OrderItem> items =
        new ArrayList<>();

    public Order(Customer customer) {
        this.customer = customer;
    }

    public void addItem(
            Product product,
            int quantity
    ) {

        items.add(
            new OrderItem(product, quantity)
        );
    }

    public double getTotal() {

        double total = 0;

        for (OrderItem item : items) {
            total += item.getSubtotal();
        }

        return total;
    }

    public void displayOrder() {

        System.out.println(
            "Customer: " + customer.getName()
        );

        for (OrderItem item : items) {

            System.out.println(
                item.getProduct().getName()
                + " x "
                + item.getQuantity()
                + " = "
                + item.getSubtotal()
            );
        }

        System.out.println(
            "Total: " + getTotal()
        );
    }
}
```

------------------------------------------------------------------------

## PaymentService

``` java
interface PaymentService {

    void pay(double amount);
}
```

``` java
class CashPayment
        implements PaymentService {

    @Override
    public void pay(double amount) {

        System.out.println(
            "Cash payment: " + amount
        );
    }
}
```

``` java
class BankPayment
        implements PaymentService {

    @Override
    public void pay(double amount) {

        System.out.println(
            "Bank payment: " + amount
        );
    }
}
```

------------------------------------------------------------------------

## Main

``` java
public class Main {

    public static void main(String[] args) {

        Customer customer =
            new Customer(
                1,
                "Nguyen Van An",
                "an@example.com"
            );

        Product shirt =
            new Product(
                1,
                "Shirt",
                250000
            );

        Product pants =
            new Product(
                2,
                "Pants",
                400000
            );

        Order order =
            new Order(customer);

        order.addItem(shirt, 2);
        order.addItem(pants, 1);

        order.displayOrder();

        PaymentService payment =
            new BankPayment();

        payment.pay(
            order.getTotal()
        );
    }
}
```

## Giải thích kiến trúc Bài 5

Bài này kết hợp gần như toàn bộ kiến thức:

``` text
Customer ─────┐
              │
Product ──> OrderItem ──> Order
                           │
                           │ getTotal()
                           ▼
                     PaymentService
                      /           \
                     /             \
             CashPayment       BankPayment
```

### Class

``` text
Product
Customer
OrderItem
Order
CashPayment
BankPayment
```

đều là class.

### Object

``` java
new Product(...)
new Customer(...)
new Order(...)
```

tạo object.

### Encapsulation

Các field:

``` java
private
```

và object cung cấp API phù hợp:

``` java
addItem()
getTotal()
getSubtotal()
```

### Composition

`Order` **HAS-A** `Customer` và chứa các `OrderItem`.

`OrderItem` **HAS-A** `Product`.

``` text
Order
 ├── Customer
 └── List<OrderItem>
          │
          └── Product
```

Đây là composition/association, không cần ép mọi quan hệ thành
inheritance.

### Abstraction

``` java
PaymentService
```

định nghĩa contract thanh toán.

### Polymorphism

``` java
PaymentService payment =
    new BankPayment();
```

hoặc:

``` java
PaymentService payment =
    new CashPayment();
```

Cùng type:

``` java
PaymentService
```

nhưng có nhiều implementation.

------------------------------------------------------------------------

# 🎯 Lộ trình học sau README này

Sau khi hiểu tài liệu, nên học theo thứ tự:

``` text
Java Basic
    ↓
Class / Object
    ↓
Constructor / Method
    ↓
Encapsulation
    ↓
Inheritance
    ↓
Polymorphism
    ↓
Abstraction
    ↓
Interface
    ↓
Composition
    ↓
Collections
    ↓
Exception
    ↓
Generics
    ↓
SOLID
    ↓
Spring Boot
```

Khi sang Spring Boot, bạn sẽ gặp lại OOP ở khắp nơi:

``` text
Controller
    ↓
Service
    ↓
ServiceImpl
    ↓
Repository
    ↓
Entity
```

OOP lúc này không còn chỉ là:

``` java
class Dog extends Animal
```

mà trở thành cách bạn **chia trách nhiệm, quản lý dependency và thiết kế
toàn bộ ứng dụng**.

------------------------------------------------------------------------

# 🧠 Câu cần nhớ

``` text
Class        = Bản thiết kế
Object       = Thực thể được tạo từ class
Attribute    = Object có gì
Method       = Object làm gì
Constructor  = Object được khởi tạo thế nào

Encapsulation
= Kiểm soát state và cách truy cập

Inheritance
= IS-A

Composition
= HAS-A

Polymorphism
= Một type, nhiều implementation/hình thái

Abstraction
= Expose điều cần dùng, ẩn chi tiết implementation

Interface
= Contract
```

> **Đừng chỉ học cú pháp OOP. Hãy tập hỏi: Object này chịu trách nhiệm
> gì? Ai được phép thay đổi state của nó? Thành phần này nên phụ thuộc
> vào class cụ thể hay abstraction? Quan hệ này thật sự là IS-A hay
> HAS-A?**
