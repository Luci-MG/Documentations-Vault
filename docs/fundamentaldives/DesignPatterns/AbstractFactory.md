# **Abstract Factory Design Pattern**

The **Abstract Factory Pattern** is a **creational design pattern** that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It promotes **loose coupling** between client code and the actual implementations, allowing the code to be more flexible and scalable.

---

## **What ?**

The Abstract Factory pattern works as a **super-factory** that creates other factories. Each factory produced by the abstract factory is responsible for creating a family of related objects. This pattern is used when a system needs to create multiple families of related objects but doesn’t want to tightly couple the code to specific implementations.

#### **Key Characteristics**
- Encapsulates the creation logic of families of related objects.
- Supports **product families** (like buttons and scrollbars for different OS themes).
- Makes the system **open for extension** but closed for modification (Open-Closed Principle).
- Clients interact with the **factory interface** instead of the concrete classes.

#### **Class Diagram**

Below is a conceptual **UML diagram** of the pattern:

```
AbstractFactory
 ├── createProductA()
 └── createProductB()

ConcreteFactory1 ────> ProductA1, ProductB1
ConcreteFactory2 ────> ProductA2, ProductB2

Client ────────> AbstractFactory, AbstractProduct
```

---

## **When to Use ?**

- When your application needs to create a **family of related objects** (e.g., GUI components for themes, or different database connections).
- When the code should be **decoupled from the actual product classes**.
- If you need to **switch between different configurations** (e.g., Light vs Dark theme).

---

## **Advantages**

- **Promotes Code Reusability** Abstract factories make it easy to reuse code across product families.
- **Supports the Open/Closed Principle** You can introduce new product families without modifying existing code.
- **Encourages Loose Coupling** Reduces dependencies between client code and the actual implementation of products.
- **Easy Maintenance** Since product creation logic is centralized, maintenance is simpler.

---

## **Disadvantages**

1. **Increased Complexity:** The pattern introduces multiple classes and interfaces, which can make the design more complex.
2. **Too Many Factories:** If there are too many products or product families, maintaining multiple factories may become cumbersome.
3. **Not Ideal for Simple Use-Cases:** For simple object creation tasks, other patterns like Factory Method or just using constructors may be more suitable.

---

## **How to Implement ?**

### **Simple Java Example**

Let’s go with an **example** Imagine you are creating a **UI component factory**. Your application can switch between two themes: **Dark Theme** and **Light Theme**. Both themes provide the same types of components (buttons, text fields) but with different appearances.

```java title="Step-1: Define the Abstract Products"
// Abstract Product: Button
public interface Button {
    void render();
}

// Abstract Product: TextField
public interface TextField {
    void render();
}
```

```java title="Step-2: Create Concrete Products"
// Concrete Product: Light Button
public class LightButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a Light Button");
    }
}

// Concrete Product: Dark Button
public class DarkButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a Dark Button");
    }
}

// Concrete Product: Light TextField
public class LightTextField implements TextField {
    @Override
    public void render() {
        System.out.println("Rendering a Light Text Field");
    }
}

// Concrete Product: Dark TextField
public class DarkTextField implements TextField {
    @Override
    public void render() {
        System.out.println("Rendering a Dark Text Field");
    }
```


```java title="Step-3:  Define the Abstract Factory Interface"
public interface UIFactory {
    Button createButton();
    TextField createTextField();
}
```

```java title="Step-4: Implement Concrete Factories"
// Concrete Factory for Light Theme
public class LightUIFactory implements UIFactory {
    @Override
    public Button createButton() {
        return new LightButton();
    }

    @Override
    public TextField createTextField() {
        return new LightTextField();
    }
}

// Concrete Factory for Dark Theme
public class DarkUIFactory implements UIFactory {
    @Override
    public Button createButton() {
        return new DarkButton();
    }

    @Override
    public TextField createTextField() {
        return new DarkTextField();
    }
}
```

```java title="Step-5: Using the Abstract Factory in a Client"
public class Application {
    private Button button;
    private TextField textField;

    public Application(UIFactory factory) {
        this.button = factory.createButton();
        this.textField = factory.createTextField();
    }

    public void renderUI() {
        button.render();
        textField.render();
    }

    public static void main(String[] args) {
        // Client can choose between different factories.
        UIFactory factory = new DarkUIFactory(); // Could be switched to LightUIFactory
        Application app = new Application(factory);
        app.renderUI();
    }
}
```

**Output:**
```
Rendering a Dark Button
Rendering a Dark Text Field
```

---

### **Spring Boot Example**

In Spring Boot, the **Abstract Factory pattern** can complement **dependency injection (DI)** by delegating object creation logic to the factory. Here’s how to **implement it with Spring Boot**.

```java title="Step-1: Define Factory Beans"
@Configuration
public class UIFactoryConfig {
    
    @Bean
    public UIFactory uiFactory(@Value("${app.theme}") String theme) {
        if ("dark".equalsIgnoreCase(theme)) {
            return new DarkUIFactory();
        } else {
            return new LightUIFactory();
        }
    }
}
```

```java title="Step-2: Use the Factory in a Controller"
@RestController
@RequestMapping("/ui")
public class UIController {

    private final UIFactory uiFactory;

    @Autowired
    public UIController(UIFactory uiFactory) {
        this.uiFactory = uiFactory;
    }

    @GetMapping("/render")
    public void renderUI() {
        Button button = uiFactory.createButton();
        TextField textField = uiFactory.createTextField();
        
        button.render();
        textField.render();
    }
}
```

```properties title="Step-3: Configure Application Properties"
# application.properties
app.theme=dark
```

In this example, the theme is configured through the `application.properties` file, and the **factory selection** is handled by the Spring context.

---

## **Comparison with Factory Method**

| **Aspect**            | **Factory Method**                   | **Abstract Factory**                 |
|-----------------------|---------------------------------------|--------------------------------------|
| **Purpose**           | Create one type of product.          | Create families of related products. |
| **Complexity**        | Less complex.                        | More complex, involves multiple classes. |
| **Client Knowledge**  | Client knows about individual products. | Client works with factories, not specific products. |
| **Usage**             | Simple use-cases.                    | Complex, multi-product scenarios.   |

---

## **Summary**

The **Abstract Factory Pattern** is a powerful tool when designing systems that need to create multiple families of related objects. While it adds complexity, the benefits include **extensibility**, **maintainability**, and **loose coupling**. In a Spring Boot application, it works well alongside **dependency injection**, especially when configurations like themes or environments vary.

---