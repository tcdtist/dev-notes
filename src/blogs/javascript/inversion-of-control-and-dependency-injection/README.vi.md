# Đảo Ngược Sự Kiểm Soát (IoC) và Tiêm Phụ Thuộc (DI) trong JavaScript

![Đảo Ngược Sự Kiểm Soát (IoC) và Tiêm Phụ Thuộc (DI) trong JavaScript](https://miro.medium.com/v2/resize:fit:602/0*eQXK-dJH0TxtSEV3.png)

Đảo Ngược Sự Kiểm Soát (IoC) và Tiêm Phụ Thuộc (DI) là các mẫu thiết kế cơ bản trong kiến trúc phần mềm giúp quản lý các phụ thuộc, từ đó thúc đẩy sự lỏng lẻo về mối liên kết và tăng cường tính mô-đun.

## Đảo Ngược Sự Kiểm Soát (IoC)

![Đảo Ngược Sự Kiểm Soát (IoC)](https://miro.medium.com/v2/resize:fit:1400/1*Si6nbljDclaUzQp28cA09w.png)

### Giải thích

Đảo Ngược Sự Kiểm Soát là một nguyên tắc trong kỹ thuật phần mềm, quy định rằng sự kiểm soát đối với các đối tượng hoặc các phần của chương trình nên được chuyển giao cho một khung làm việc hoặc container, trái ngược với việc gọi thủ tục truyền thống nơi sự kiểm soát thuộc về chính chương trình.

Hãy tưởng tượng bạn đang đi rửa xe. Trong kịch bản truyền thống, bạn tự làm mọi việc từ thu thập dụng cụ, chà rửa xe, xả nước và lau khô. Điều này giống như việc kiểm soát mọi phần của code trong một chương trình phần mềm thông thường.

Bây giờ, hãy áp dụng IoC vào kịch bản của chúng ta. Bạn quyết định đưa xe của mình đến một dịch vụ rửa xe chuyên nghiệp thay vì tự làm. Tại đây, bạn chỉ cần lái xe vào, trả tiền cho dịch vụ và nhân viên rửa xe sẽ làm hết mọi việc cho bạn. Bạn đã đảo ngược sự kiểm soát trong tình huống này. Bạn đã giao trách nhiệm rửa xe cho dịch vụ rửa xe.

Trong phát triển phần mềm, IoC cho phép chúng ta chuyển sự kiểm soát từ code của chúng ta sang một khung làm việc bên ngoài. Bằng cách áp dụng IoC, chúng ta có thể tập trung vào việc định nghĩa "cái gì" trong khi để khung làm việc xử lý "làm thế nào".

### Ví dụ

```jsx
// Cách tiếp cận truyền thống
class Car {
  start() {
    this.engine.start();
  }
}

// Cách tiếp cận IoC
class Car {
  constructor(engine) {
    this.engine = engine;
  }

  start() {
    this.engine.start();
  }
}

const car = new Car(new Engine());
car.start();
```

Ở đây, lớp `Car` không tạo một thể hiện của `Engine` mà chính nó nhưng lại được tiêm vào, cho phép linh hoạt hơn và dễ dàng kiểm thử hơn.

## Nguyên Tắc Đảo Ngược Phụ Thuộc (DIP)

![Nguyên Tắc Đảo Ngược Phụ Thuộc (DIP)](https://media.licdn.com/dms/image/C5612AQFFFjbboRXvhw/article-cover_image-shrink_600_2000/0/1647405323448?e=2147483647&v=beta&t=RAPpylzq5sBfKXy4kwiPZlI2DUzJktln3xQQmEQW6CI)

### Giải thích

Nguyên tắc Đảo Ngược Phụ Thuộc là một chiến lược để giảm sự phụ thuộc giữa các mô-đun phần mềm. Nguyên tắc này nói rằng các mô-đun cấp cao không nên phụ thuộc vào các mô-đun cấp thấp. Thay vào đó, cả hai nên phụ thuộc vào trừu tượng.

### Ví dụ

```jsx
// Mô-đun cấp thấp
class EmailService {
  send(to, message) {
    console.log(`Sending an email to ${to}: ${message}`);
  }
}

// Mô-đun cấp cao phụ thuộc vào một trừu tượng
class NotificationService {
  constructor(emailService) {
    this.emailService = emailService;
  }

  notify(user, message) {
    this.emailService.send(user.email, message);
  }
}

// Phụ thuộc được truyền vào mô-đun cấp cao
const emailService = new EmailService();
const notificationService = new NotificationService(emailService);
notificationService.notify({ email: "user@example.com" }, "Welcome!");
```

## Tiêm Phụ Thuộc (DI)

![Tiêm Phụ Thuộc (DI)](https://stackify.com/wp-content/uploads/2018/06/Design-Patterns-Explained-%E2%80%93-Dependency-Injection-with-Code-Examples-881x440-1.png)

### Giải thích

Tiêm Phụ Thuộc là một mẫu thiết kế được sử dụng để thực hiện IoC, cho phép tạo ra các đối tượng phụ thuộc bên ngoài lớp và cung cấp những đối tượng này cho lớp thông qua các cách khác nhau như tiêm qua hàm tạo, phương thức hoặc thuộc tính.

### Ví dụ

```jsx
// Tiêm qua hàm tạo
class UserService {
  constructor(emailService) {
    this.emailService = emailService;
  }

  register(user) {
    // Đăng ký người dùng
    this.emailService.send(user.email, "Chào mừng bạn đến với hệ thống!");
  }
}

const emailService = new EmailService();
const userService = new UserService(emailService);
userService.register({ email: "john@example.com" });
```

## Kết Luận

Bằng cách sử dụng IoC và DI, các nhà phát triển có thể tạo ra các hệ thống mô-đun, dễ kiểm thử và bảo trì. IoC đảo ngược sự kiểm soát, cho phép các khung làm việc đảm nhận,
trong khi DI cung cấp sự linh hoạt trong cách quản lý các phụ thuộc. Cùng nhau, các mẫu thiết kế này cho phép bạn xây dựng các hệ thống nơi các thành phần dễ dàng thay thế và phát triển trở nên dễ quản lý và mở rộng hơn.

Những thực tiễn này đặc biệt có lợi trong các ứng dụng phức tạp, nơi quản lý các phụ thuộc theo cách truyền thống có thể dẫn đến code chặt chẽ khó quản lý và phát triển.

### Các Thực Tiễn Được Khuyến Nghị

1. **Sử dụng các khung làm việc hỗ trợ DI**: Trong JavaScript, các khung làm việc như Angular đi kèm với tiêm phụ thuộc tích hợp sẵn.
2. **Tận dụng các container IoC**: Các thư viện như InversifyJS có thể giúp quản lý IoC trong các ứng dụng lớn hơn.

Bằng cách áp dụng các nguyên tắc này, các nhà phát triển có thể giảm đáng kể mức độ phụ thuộc giữa các thành phần và tăng cường khả năng chống chịu với các thay đổi của hệ thống, dẫn đến một cơ sở mã nguồn mạnh mẽ và dễ bảo trì hơn.

## Tài liệu đọc thêm:

- [Inversion of Control (IoC) and Dependency Injection (DI)](https://medium.com/@kadriozcan/inversion-of-control-and-dependency-injection-6e6f628c6a06)
- [Serries DEPENDENCY INJECTION VÀ INVERSION OF CONTROL](https://toidicodedao.com/2015/11/03/dependency-injection-va-inversion-of-control-phan-1-dinh-nghia/)

---

Nếu bạn thấy bài viết này hữu ích, vui lòng tặng cho tôi một ngôi sao trên [GitHub](https://github.com/tcdtist/public-clean-code)!
