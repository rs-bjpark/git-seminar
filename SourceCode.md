// ===============================
// Chapter 1-2: Hello Git & Calculator 프로젝트
// ===============================

// Hello.java - 첫 번째 Git 실습용
public class Hello {
private String message;

    public Hello() {
        this.message = "Hello Git!";
    }
    
    public Hello(String message) {
        this.message = message;
    }
    
    public void sayHello() {
        System.out.println(message);
    }
    
    public void sayHelloWithTime() {
        System.out.println(message + " - " + java.time.LocalDateTime.now());
    }
    
    public static void main(String[] args) {
        Hello hello = new Hello();
        hello.sayHello();
        
        Hello customHello = new Hello("Learning Git is awesome!");
        customHello.sayHelloWithTime();
    }
}

// Calculator.java - Git 브랜치 실습용
public class Calculator {
private static final String VERSION = "1.0.0";

    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
    
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public double divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Cannot divide by zero");
        }
        return (double) a / b;
    }
    
    // Chapter 3에서 브랜치별로 추가할 기능들
    // feature/advanced-operations 브랜치에서 추가
    public double power(double base, double exponent) {
        return Math.pow(base, exponent);
    }
    
    public double sqrt(double number) {
        if (number < 0) {
            throw new IllegalArgumentException("Cannot calculate square root of negative number");
        }
        return Math.sqrt(number);
    }
    
    // feature/memory-functions 브랜치에서 추가
    private double memory = 0;
    
    public void memoryStore(double value) {
        this.memory = value;
    }
    
    public double memoryRecall() {
        return this.memory;
    }
    
    public void memoryClear() {
        this.memory = 0;
    }
    
    public String getVersion() {
        return VERSION;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        // 기본 연산 테스트
        System.out.println("Calculator v" + calc.getVersion());
        System.out.println("2 + 3 = " + calc.add(2, 3));
        System.out.println("5 - 2 = " + calc.subtract(5, 2));
        System.out.println("4 * 6 = " + calc.multiply(4, 6));
        System.out.println("10 / 2 = " + calc.divide(10, 2));
        
        // 고급 연산 테스트 (브랜치에서 추가될 예정)
        System.out.println("2^3 = " + calc.power(2, 3));
        System.out.println("√16 = " + calc.sqrt(16));
        
        // 메모리 기능 테스트 (브랜치에서 추가될 예정)
        calc.memoryStore(42);
        System.out.println("Memory: " + calc.memoryRecall());
    }
}

// CalculatorTest.java - TDD 실습용
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
private Calculator calculator;

    @BeforeEach
    public void setUp() {
        calculator = new Calculator();
    }
    
    // 기본 연산 테스트
    @Test
    public void testAdd() {
        assertEquals(5, calculator.add(2, 3));
        assertEquals(-1, calculator.add(-2, 1));
        assertEquals(0, calculator.add(0, 0));
    }
    
    @Test
    public void testSubtract() {
        assertEquals(1, calculator.subtract(3, 2));
        assertEquals(-3, calculator.subtract(-1, 2));
        assertEquals(5, calculator.subtract(5, 0));
    }
    
    @Test
    public void testMultiply() {
        assertEquals(6, calculator.multiply(2, 3));
        assertEquals(-6, calculator.multiply(-2, 3));
        assertEquals(0, calculator.multiply(5, 0));
    }
    
    @Test
    public void testDivide() {
        assertEquals(2.0, calculator.divide(4, 2), 0.001);
        assertEquals(2.5, calculator.divide(5, 2), 0.001);
    }
    
    @Test
    public void testDivideByZero() {
        assertThrows(IllegalArgumentException.class, 
                    () -> calculator.divide(1, 0));
    }
    
    // 고급 연산 테스트 (브랜치에서 추가될 예정)
    @Test
    public void testPower() {
        assertEquals(8.0, calculator.power(2, 3), 0.001);
        assertEquals(1.0, calculator.power(5, 0), 0.001);
        assertEquals(25.0, calculator.power(5, 2), 0.001);
    }
    
    @Test
    public void testSqrt() {
        assertEquals(4.0, calculator.sqrt(16), 0.001);
        assertEquals(0.0, calculator.sqrt(0), 0.001);
        assertEquals(1.0, calculator.sqrt(1), 0.001);
    }
    
    @Test
    public void testSqrtNegative() {
        assertThrows(IllegalArgumentException.class, 
                    () -> calculator.sqrt(-1));
    }
    
    // 메모리 기능 테스트 (브랜치에서 추가될 예정)
    @Test
    public void testMemoryFunctions() {
        assertEquals(0, calculator.memoryRecall()); // 초기값
        
        calculator.memoryStore(42);
        assertEquals(42, calculator.memoryRecall());
        
        calculator.memoryStore(100);
        assertEquals(100, calculator.memoryRecall());
        
        calculator.memoryClear();
        assertEquals(0, calculator.memoryRecall());
    }
}

// ===============================
// Chapter 3, 5: 사용자 관리 시스템
// ===============================

// User.java
public class User {
private String id;
private String username;
private String email;
private String password;
private java.time.LocalDateTime createdAt;
private boolean active;

    public User(String id, String username, String email, String password) {
        this.id = id;
        this.username = username;
        this.email = email;
        this.password = password;
        this.createdAt = java.time.LocalDateTime.now();
        this.active = true;
    }
    
    // Getters and Setters
    public String getId() { return id; }
    public void setId(String id) { this.id = id; }
    
    public String getUsername() { return username; }
    public void setUsername(String username) { this.username = username; }
    
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
    
    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }
    
    public java.time.LocalDateTime getCreatedAt() { return createdAt; }
    
    public boolean isActive() { return active; }
    public void setActive(boolean active) { this.active = active; }
    
    @Override
    public String toString() {
        return String.format("User{id='%s', username='%s', email='%s', active=%s}", 
                           id, username, email, active);
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        User user = (User) obj;
        return id != null ? id.equals(user.id) : user.id == null;
    }