# Inversion of Control (IoC) and Dependency Injection (DI) in JavaScript

![Inversion of Control (IoC) and Dependency Injection (DI) in JavaScript](https://miro.medium.com/v2/resize:fit:602/0*eQXK-dJH0TxtSEV3.png)

Inversion of Control (IoC) and Dependency Injection (DI) are fundamental design patterns in software architecture that help manage dependencies, thus promoting loose coupling and greater modularity.

## Inversion of Control (IoC)

![Inversion of Control (IoC)](https://miro.medium.com/v2/resize:fit:1400/1*Si6nbljDclaUzQp28cA09w.png)

### Explanation

Inversion of Control is a principle in software engineering which dictates that the control of objects or portions of a program should be transferred to a container or framework — contrast to traditional procedure call where the control is with the program itself.

Imagine you are operating a car wash. In a traditional scenario, you manually wash your car, controlling every step of the process. Now, consider the IoC approach where you drive your car to a professional service. Here, you hand over the control of washing your car to the service. Just like this scenario, in software development, IoC allows you to reduce dependencies by delegating control to frameworks or containers.

### Example

```jsx
// Traditional approach
class Car {
  start() {
    this.engine.start();
  }
}

// IoC approach
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

Here, the `Car` class does not create an instance of `Engine` itself but rather, it's injected, allowing for better flexibility and easier testing.

## Dependency Inversion Principle (DIP)

![Dependency Inversion Principle (DIP)](https://media.licdn.com/dms/image/C5612AQFFFjbboRXvhw/article-cover_image-shrink_600_2000/0/1647405323448?e=2147483647&v=beta&t=RAPpylzq5sBfKXy4kwiPZlI2DUzJktln3xQQmEQW6CI)

### Explanation

Dependency Inversion Principle is a strategy to decouple software modules. This principle states that high-level modules should not depend on low-level modules, but both should depend on abstractions.

### Example

```jsx
// Low-level module
class EmailService {
  send(to, message) {
    console.log(`Sending an email to ${to}: ${message}`);
  }
}

// High-level module depending on an abstraction
class NotificationService {
  constructor(emailService) {
    this.emailService = emailService;
  }

  notify(user, message) {
    this.emailService.send(user.email, message);
  }
}

// Dependency is passed to the high-level module
const emailService = new EmailService();
const notificationService = new NotificationService(emailService);
notificationService.notify({ email: "user@example.com" }, "Welcome!");
```

## Dependency Injection (DI)

![Dependency Injection (DI)](https://stackify.com/wp-content/uploads/2018/06/Design-Patterns-Explained-%E2%80%93-Dependency-Injection-with-Code-Examples-881x440-1.png)

### Explanation

Dependency Injection is a design pattern used to implement IoC, allowing the creation of dependent objects outside of a class and providing those objects to a class through different ways such as constructor injection, method injection, or property injection.

### Example

```jsx
// Constructor injection
class UserService {
  constructor(emailService) {
    this.emailService = emailService;
  }

  register(user) {
    // Register the user
    this.emailService.send(user.email, "Welcome to the system!");
  }
}

const emailService = new EmailService();
const userService = new UserService(emailService);
userService.register({ email: "john@example.com" });
```

## Conclusion

By utilizing IoC and DI, developers can create systems that are modular, easy to test, and maintain. IoC inverts the control, allowing frameworks to take charge, while DI provides flexibility in how dependencies are managed. Together, these patterns enable you to build systems where components are easily interchangeable and development becomes more manageable and scalable.

These practices are especially beneficial in complex applications where managing the dependencies in a traditional way can lead to tightly coupled code that is hard to manage and evolve.

### Recommended Practices

1. **Use frameworks that support DI**: In JavaScript, frameworks like Angular come with built-in dependency injection.
2. **Leverage IoC containers**: Libraries such as InversifyJS can help manage IoC in larger applications.

By adopting these principles, developers can significantly reduce the coupling between components and increase the system's resilience to changes, leading to a more robust and maintainable codebase.

## Additional reading material:

- [Inversion of Control (IoC) and Dependency Injection (DI)](https://medium.com/@kadriozcan/inversion-of-control-and-dependency-injection-6e6f628c6a06)
- [Serries DEPENDENCY INJECTION VÀ INVERSION OF CONTROL](https://toidicodedao.com/2015/11/03/dependency-injection-va-inversion-of-control-phan-1-dinh-nghia/)

---

If you found this article helpful, please give me a star on [GitHub](https://github.com/tcdtist/public-clean-code)!
