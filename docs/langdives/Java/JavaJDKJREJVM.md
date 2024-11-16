# Java

## 1. Intro

Java is a high-level, object-oriented programming language designed for portability, security, and ease of use. It is known for its "write once, run anywhere" capability, allowing developers to create software that can run on any device with a Java Virtual Machine (JVM).

---

## 2. Architecture

The Java architecture is composed of three main components:

### 2.1 Java Development Kit (JDK)

**Definition**: The JDK is a comprehensive development environment for building Java applications. It provides all the tools necessary for Java developers to create, compile, and package Java applications.

**Components**:
- **Java Compiler (`javac`)**:  Translates Java source code (files with a `.java` extension) into bytecode (files with a `.class` extension).
- **Java Runtime Environment (JRE)**: A subset of the JDK, required to run Java applications.
- **Development Tools**: Tools for debugging, monitoring, and managing Java applications, such as `javadoc`, `jdb`, and `jar`.

### 2.2 Java Runtime Environment (JRE)

**Definition**: The JRE provides the libraries, Java Virtual Machine (JVM), and other components necessary for running Java applications. It does not include development tools, making it ideal for end-users who only need to run Java applications.

**Components**:
- **Java Virtual Machine (JVM)**: The core component that executes Java bytecode.
- **Java Class Libraries**: Precompiled libraries containing standard Java classes used for various functionalities.

### 2.3 Java Virtual Machine (JVM)

**Definition**: The JVM is an abstract computing machine that enables a computer to run Java programs. It is responsible for interpreting and executing the bytecode generated by the Java compiler.

**Functions**:
- **Loading**: Loads `.class` files containing the bytecode into memory.
- **Linking**: Combines and prepares the bytecode for execution by resolving references and validating the code.
- **Execution**: Translates bytecode into machine code specific to the operating system, allowing the application to run.

---

## 3. How It Works

The execution of Java code involves several steps, transitioning through the JDK, JRE, and JVM before reaching the machine code that the computer's CPU executes.

**3.1 Code Writing** : Java developers write source code in plain text files using the `.java` extension. This code defines classes and methods that make up the Java application.

**3.2 Code Compilation**:

- The developer uses the Java compiler (`javac`), which is part of the JDK, to compile the `.java` file. This process translates the human-readable Java code into an intermediate form known as bytecode.
- The output of this step is a `.class` file containing the bytecode.

**3.3 Running the Application**:

- To run the Java application, the developer executes a command using the Java runtime environment (e.g., `java ClassName`), which triggers the JRE.
- The JRE includes the JVM, which performs the following steps:

**3.3.1 Loading**: The JVM locates the specified `.class` file and loads it into memory.

**3.3.2 Linking**: The JVM links the bytecode:
  - **Verification**: Ensures the bytecode adheres to the JVM specifications, checking for security and integrity.
  - **Preparation**: Allocates memory for static variables and prepares the code for execution.
  - **Resolution**: Resolves symbolic references to classes, methods, and fields.

**3.3.3 Execution**: The JVM executes the bytecode:
  - **Interpreting**: The JVM can interpret the bytecode line-by-line, converting it to machine code as it runs.
  - **JIT Compilation**: For performance optimization, the JVM employs a Just-In-Time (JIT) compiler, which compiles frequently executed bytecode into native machine code at runtime. This compiled code is stored in memory for future calls, improving execution speed.

**3.4 Machine Code Execution**: The machine code generated by the JVM is executed by the host operating system's CPU. This process allows Java applications to be platform-independent, as the same bytecode can run on any system that has a compatible JVM.

---

## 4. Hierarchical Structure

The hierarchy of Java components can be visualized as follows:

```
JDK (includes JRE)
└── JRE (includes JVM and libraries)
    └── JVM (executes bytecode)
```

---