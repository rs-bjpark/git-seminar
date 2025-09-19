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
    
    @Override
    public int hashCode() {
        return id != null ? id.hashCode() : 0;
    }
}

// UserService.java - feature/user-management 브랜치에서 개발
import java.util.*;
import java.util.stream.Collectors;

public class UserService {
private Map<String, User> users = new HashMap<>();
private Set<String> usedEmails = new HashSet<>();

    public boolean register(User user) {
        // 사용자명 중복 체크
        if (users.containsKey(user.getUsername())) {
            throw new IllegalArgumentException("Username already exists: " + user.getUsername());
        }
        
        // 이메일 중복 체크
        if (usedEmails.contains(user.getEmail())) {
            throw new IllegalArgumentException("Email already registered: " + user.getEmail());
        }
        
        // 비밀번호 유효성 검사
        if (!isValidPassword(user.getPassword())) {
            throw new IllegalArgumentException("Password does not meet requirements");
        }
        
        users.put(user.getUsername(), user);
        usedEmails.add(user.getEmail());
        return true;
    }
    
    public boolean login(String username, String password) {
        User user = users.get(username);
        if (user == null) {
            return false;
        }
        
        if (!user.isActive()) {
            throw new IllegalStateException("User account is deactivated");
        }
        
        return user.getPassword().equals(password);
    }
    
    public User findUser(String username) {
        return users.get(username);
    }
    
    public List<User> getAllUsers() {
        return new ArrayList<>(users.values());
    }
    
    public List<User> getActiveUsers() {
        return users.values().stream()
                   .filter(User::isActive)
                   .collect(Collectors.toList());
    }
    
    public boolean deactivateUser(String username) {
        User user = users.get(username);
        if (user != null) {
            user.setActive(false);
            return true;
        }
        return false;
    }
    
    public boolean activateUser(String username) {
        User user = users.get(username);
        if (user != null) {
            user.setActive(true);
            return true;
        }
        return false;
    }
    
    public boolean updatePassword(String username, String oldPassword, String newPassword) {
        User user = users.get(username);
        if (user == null || !user.getPassword().equals(oldPassword)) {
            return false;
        }
        
        if (!isValidPassword(newPassword)) {
            throw new IllegalArgumentException("New password does not meet requirements");
        }
        
        user.setPassword(newPassword);
        return true;
    }
    
    private boolean isValidPassword(String password) {
        // 최소 8자, 숫자와 문자 포함
        return password != null && 
               password.length() >= 8 && 
               password.matches(".*\\d.*") && 
               password.matches(".*[a-zA-Z].*");
    }
    
    public int getUserCount() {
        return users.size();
    }
    
    public int getActiveUserCount() {
        return (int) users.values().stream().filter(User::isActive).count();
    }
}

// AuthenticationService.java - feature/authentication 브랜치에서 개발
import java.time.LocalDateTime;
import java.util.*;

public class AuthenticationService {
private UserService userService;
private Map<String, String> activeSessions = new HashMap<>();
private Map<String, LocalDateTime> sessionExpiry = new HashMap<>();
private Map<String, Integer> loginAttempts = new HashMap<>();
private static final int MAX_LOGIN_ATTEMPTS = 5;
private static final int SESSION_TIMEOUT_MINUTES = 30;

    public AuthenticationService(UserService userService) {
        this.userService = userService;
    }
    
    public String authenticate(String username, String password) {
        // 로그인 시도 횟수 체크
        if (isAccountLocked(username)) {
            throw new IllegalStateException("Account is temporarily locked due to too many failed attempts");
        }
        
        try {
            if (userService.login(username, password)) {
                // 로그인 성공 시 세션 생성
                String sessionId = generateSessionId();
                activeSessions.put(sessionId, username);
                sessionExpiry.put(sessionId, LocalDateTime.now().plusMinutes(SESSION_TIMEOUT_MINUTES));
                
                // 로그인 시도 횟수 초기화
                loginAttempts.remove(username);
                
                return sessionId;
            } else {
                // 로그인 실패 시 시도 횟수 증가
                increaseLoginAttempts(username);
                return null;
            }
        } catch (Exception e) {
            increaseLoginAttempts(username);
            throw e;
        }
    }
    
    public boolean isValidSession(String sessionId) {
        if (!activeSessions.containsKey(sessionId)) {
            return false;
        }
        
        LocalDateTime expiry = sessionExpiry.get(sessionId);
        if (expiry.isBefore(LocalDateTime.now())) {
            // 세션 만료
            logout(sessionId);
            return false;
        }
        
        // 세션 연장
        sessionExpiry.put(sessionId, LocalDateTime.now().plusMinutes(SESSION_TIMEOUT_MINUTES));
        return true;
    }
    
    public String getSessionUser(String sessionId) {
        if (isValidSession(sessionId)) {
            return activeSessions.get(sessionId);
        }
        return null;
    }
    
    public void logout(String sessionId) {
        activeSessions.remove(sessionId);
        sessionExpiry.remove(sessionId);
    }
    
    public void logoutUser(String username) {
        List<String> sessionsToRemove = new ArrayList<>();
        for (Map.Entry<String, String> entry : activeSessions.entrySet()) {
            if (entry.getValue().equals(username)) {
                sessionsToRemove.add(entry.getKey());
            }
        }
        
        for (String sessionId : sessionsToRemove) {
            logout(sessionId);
        }
    }
    
    private String generateSessionId() {
        return UUID.randomUUID().toString();
    }
    
    private boolean isAccountLocked(String username) {
        return loginAttempts.getOrDefault(username, 0) >= MAX_LOGIN_ATTEMPTS;
    }
    
    private void increaseLoginAttempts(String username) {
        loginAttempts.put(username, loginAttempts.getOrDefault(username, 0) + 1);
    }
    
    public void clearLoginAttempts(String username) {
        loginAttempts.remove(username);
    }
    
    public int getActiveSessionCount() {
        // 만료된 세션 정리
        List<String> expiredSessions = new ArrayList<>();
        LocalDateTime now = LocalDateTime.now();
        
        for (Map.Entry<String, LocalDateTime> entry : sessionExpiry.entrySet()) {
            if (entry.getValue().isBefore(now)) {
                expiredSessions.add(entry.getKey());
            }
        }
        
        for (String sessionId : expiredSessions) {
            logout(sessionId);
        }
        
        return activeSessions.size();
    }
}

// ===============================
// Chapter 5, 7: 도서관 관리 시스템
// ===============================

// Book.java
public class Book {
private String id;
private String title;
private String author;
private String isbn;
private String category;
private boolean available;
private java.time.LocalDate publishDate;
private java.time.LocalDateTime addedDate;

    public Book(String id, String title, String author, String isbn, String category) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.category = category;
        this.available = true;
        this.addedDate = java.time.LocalDateTime.now();
    }
    
    // Getters and Setters
    public String getId() { return id; }
    public void setId(String id) { this.id = id; }
    
    public String getTitle() { return title; }
    public void setTitle(String title) { this.title = title; }
    
    public String getAuthor() { return author; }
    public void setAuthor(String author) { this.author = author; }
    
    public String getIsbn() { return isbn; }
    public void setIsbn(String isbn) { this.isbn = isbn; }
    
    public String getCategory() { return category; }
    public void setCategory(String category) { this.category = category; }
    
    public boolean isAvailable() { return available; }
    public void setAvailable(boolean available) { this.available = available; }
    
    public java.time.LocalDate getPublishDate() { return publishDate; }
    public void setPublishDate(java.time.LocalDate publishDate) { this.publishDate = publishDate; }
    
    public java.time.LocalDateTime getAddedDate() { return addedDate; }
    
    @Override
    public String toString() {
        return String.format("Book{id='%s', title='%s', author='%s', available=%s}", 
                           id, title, author, available);
    }
}

// BorrowRecord.java
public class BorrowRecord {
private String id;
private String userId;
private String bookId;
private java.time.LocalDateTime borrowDate;
private java.time.LocalDateTime dueDate;
private java.time.LocalDateTime returnDate;
private boolean returned;

    public BorrowRecord(String id, String userId, String bookId) {
        this.id = id;
        this.userId = userId;
        this.bookId = bookId;
        this.borrowDate = java.time.LocalDateTime.now();
        this.dueDate = borrowDate.plusDays(14); // 2주 대출
        this.returned = false;
    }
    
    // Getters and Setters
    public String getId() { return id; }
    public String getUserId() { return userId; }
    public String getBookId() { return bookId; }
    public java.time.LocalDateTime getBorrowDate() { return borrowDate; }
    public java.time.LocalDateTime getDueDate() { return dueDate; }
    public java.time.LocalDateTime getReturnDate() { return returnDate; }
    public boolean isReturned() { return returned; }
    
    public void markAsReturned() {
        this.returned = true;
        this.returnDate = java.time.LocalDateTime.now();
    }
    
    public boolean isOverdue() {
        return !returned && java.time.LocalDateTime.now().isAfter(dueDate);
    }
    
    public long getDaysOverdue() {
        if (!isOverdue()) return 0;
        return java.time.Duration.between(dueDate, java.time.LocalDateTime.now()).toDays();
    }
}

// LibraryService.java - feature/library-management 브랜치에서 개발
import java.util.*;
import java.util.stream.Collectors;

public class LibraryService {
private Map<String, Book> books = new HashMap<>();
private Map<String, BorrowRecord> borrowRecords = new HashMap<>();
private Map<String, Set<String>> userBorrowedBooks = new HashMap<>();
private int nextRecordId = 1;

    // 도서 관리
    public void addBook(Book book) {
        if (books.containsKey(book.getId())) {
            throw new IllegalArgumentException("Book with ID already exists: " + book.getId());
        }
        books.put(book.getId(), book);
    }
    
    public Book findBook(String bookId) {
        return books.get(bookId);
    }
    
    public List<Book> getAllBooks() {
        return new ArrayList<>(books.values());
    }
    
    public List<Book> getAvailableBooks() {
        return books.values().stream()
                   .filter(Book::isAvailable)
                   .collect(Collectors.toList());
    }
    
    public List<Book> searchBooks(String query) {
        String lowerQuery = query.toLowerCase();
        return books.values().stream()
                   .filter(book -> 
                       book.getTitle().toLowerCase().contains(lowerQuery) ||
                       book.getAuthor().toLowerCase().contains(lowerQuery) ||
                       book.getCategory().toLowerCase().contains(lowerQuery))
                   .collect(Collectors.toList());
    }
    
    public List<Book> getBooksByCategory(String category) {
        return books.values().stream()
                   .filter(book -> book.getCategory().equalsIgnoreCase(category))
                   .collect(Collectors.toList());
    }
    
    public List<Book> getBooksByAuthor(String author) {
        return books.values().stream()
                   .filter(book -> book.getAuthor().equalsIgnoreCase(author))
                   .collect(Collectors.toList());
    }
    
    // 대출 관리
    public BorrowRecord borrowBook(String userId, String bookId) {
        Book book = books.get(bookId);
        if (book == null) {
            throw new IllegalArgumentException("Book not found: " + bookId);
        }
        
        if (!book.isAvailable()) {
            throw new IllegalStateException("Book is not available for borrowing");
        }
        
        // 사용자가 이미 대출한 책 수 확인 (최대 5권)
        Set<String> userBooks = userBorrowedBooks.getOrDefault(userId, new HashSet<>());
        if (userBooks.size() >= 5) {
            throw new IllegalStateException("User has reached maximum borrowing limit (5 books)");
        }
        
        // 연체된 책이 있는지 확인
        if (hasOverdueBooks(userId)) {
            throw new IllegalStateException("User has overdue books. Please return them first.");
        }
        
        // 대출 처리
        String recordId = String.valueOf(nextRecordId++);
        BorrowRecord record = new BorrowRecord(recordId, userId, bookId);
        
        book.setAvailable(false);
        borrowRecords.put(recordId, record);
        userBorrowedBooks.computeIfAbsent(userId, k -> new HashSet<>()).add(bookId);
        
        return record;
    }
    
    public boolean returnBook(String userId, String bookId) {
        // 사용자가 대출한 책인지 확인
        Set<String> userBooks = userBorrowedBooks.get(userId);
        if (userBooks == null || !userBooks.contains(bookId)) {
            return false;
        }
        
        // 대출 기록 찾기
        BorrowRecord record = findActiveBorrowRecord(userId, bookId);
        if (record == null) {
            return false;
        }
        
        // 반납 처리
        Book book = books.get(bookId);
        book.setAvailable(true);
        record.markAsReturned();
        userBooks.remove(bookId);
        
        return true;
    }
    
    public List<BorrowRecord> getUserBorrowHistory(String userId) {
        return borrowRecords.values().stream()
                           .filter(record -> record.getUserId().equals(userId))
                           .sorted((r1, r2) -> r2.getBorrowDate().compareTo(r1.getBorrowDate()))
                           .collect(Collectors.toList());
    }
    
    public List<BorrowRecord> getActiveBorrowRecords(String userId) {
        return borrowRecords.values().stream()
                           .filter(record -> record.getUserId().equals(userId) && !record.isReturned())
                           .collect(Collectors.toList());
    }
    
    public List<BorrowRecord> getOverdueRecords() {
        return borrowRecords.values().stream()
                           .filter(BorrowRecord::isOverdue)
                           .collect(Collectors.toList());
    }
    
    public List<BorrowRecord> getUserOverdueRecords(String userId) {
        return borrowRecords.values().stream()
                           .filter(record -> record.getUserId().equals(userId) && record.isOverdue())
                           .collect(Collectors.toList());
    }
    
    private boolean hasOverdueBooks(String userId) {
        return borrowRecords.values().stream()
                           .anyMatch(record -> record.getUserId().equals(userId) && record.isOverdue());
    }
    
    private BorrowRecord findActiveBorrowRecord(String userId, String bookId) {
        return borrowRecords.values().stream()
                           .filter(record -> 
                               record.getUserId().equals(userId) && 
                               record.getBookId().equals(bookId) && 
                               !record.isReturned())
                           .findFirst()
                           .orElse(null);
    }
    
    // 통계 정보
    public Map<String, Object> getLibraryStatistics() {
        Map<String, Object> stats = new HashMap<>();
        
        stats.put("totalBooks", books.size());
        stats.put("availableBooks", getAvailableBooks().size());
        stats.put("borrowedBooks", books.size() - getAvailableBooks().size());
        stats.put("totalBorrowRecords", borrowRecords.size());
        stats.put("activeBorrowRecords", 
                 borrowRecords.values().stream().filter(r -> !r.isReturned()).count());
        stats.put("overdueRecords", getOverdueRecords().size());
        
        // 카테고리별 통계
        Map<String, Long> categoryStats = books.values().stream()
            .collect(Collectors.groupingBy(Book::getCategory, Collectors.counting()));
        stats.put("booksByCategory", categoryStats);
        
        return stats;
    }
}

// ===============================
// 테스트 클래스들
// ===============================

// UserServiceTest.java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import static org.junit.jupiter.api.Assertions.*;

public class UserServiceTest {
private UserService userService;

    @BeforeEach
    public void setUp() {
        userService = new UserService();
    }
    
    @Test
    public void testUserRegistration() {
        User user = new User("1", "john_doe", "john@example.com", "password123");
        assertTrue(userService.register(user));
        assertEquals(1, userService.getUserCount());
    }
    
    @Test
    public void testDuplicateUsername() {
        User user1 = new User("1", "john_doe", "john@example.com", "password123");
        User user2 = new User("2", "john_doe", "jane@example.com", "password456");
        
        userService.register(user1);
        assertThrows(IllegalArgumentException.class, () -> userService.register(user2));
    }
    
    @Test
    public void testDuplicateEmail() {
        User user1 = new User("1", "john_doe", "john@example.com", "password123");
        User user2 = new User("2", "jane_doe", "john@example.com", "password456");
        
        userService.register(user1);
        assertThrows(IllegalArgumentException.class, () -> userService.register(user2));
    }
    
    @Test
    public void testInvalidPassword() {
        User user = new User("1", "john_doe", "john@example.com", "123"); // Too short
        assertThrows(IllegalArgumentException.class, () -> userService.register(user));
    }
    
    @Test
    public void testLogin() {
        User user = new User("1", "john_doe", "john@example.com", "password123");
        userService.register(user);
        
        assertTrue(userService.login("john_doe", "password123"));
        assertFalse(userService.login("john_doe", "wrongpassword"));
        assertFalse(userService.login("nonexistent", "password123"));
    }
    
    @Test
    public void testUserDeactivation() {
        User user = new User("1", "john_doe", "john@example.com", "password123");
        userService.register(user);
        
        assertTrue(userService.deactivateUser("john_doe"));
        assertThrows(IllegalStateException.class, 
                    () -> userService.login("john_doe", "password123"));
    }
}

// LibraryServiceTest.java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import static org.junit.jupiter.api.Assertions.*;

public class LibraryServiceTest {
private LibraryService libraryService;

    @BeforeEach
    public void setUp() {
        libraryService = new LibraryService();
    }
    
    @Test
    public void testAddBook() {
        Book book = new Book("1", "Java Programming", "John Smith", "978-0123456789", "Programming");
        libraryService.addBook(book);
        
        assertEquals(book, libraryService.findBook("1"));
        assertEquals(1, libraryService.getAllBooks().size());
    }
    
    @Test
    public void testBorrowBook() {
        Book book = new Book("1", "Java Programming", "John Smith", "978-0123456789", "Programming");
        libraryService.addBook(book);
        
        BorrowRecord record = libraryService.borrowBook("user1", "1");
        assertNotNull(record);
        assertFalse(book.isAvailable());
        assertEquals("user1", record.getUserId());
        assertEquals("1", record.getBookId());
    }
    
    @Test
    public void testReturnBook() {
        Book book = new Book("1", "Java Programming", "John Smith", "978-0123456789", "Programming");
        libraryService.addBook(book);
        
        libraryService.borrowBook("user1", "1");
        assertTrue(libraryService.returnBook("user1", "1"));
        assertTrue(book.isAvailable());
    }
    
    @Test
    public void testBorrowUnavailableBook() {
        Book book = new Book("1", "Java Programming", "John Smith", "978-0123456789", "Programming");
        libraryService.addBook(book);
        
        libraryService.borrowBook("user1", "1");
        assertThrows(IllegalStateException.class, 
                    () -> libraryService.borrowBook("user2", "1"));
    }
    
    @Test
    public void testSearchBooks() {
        Book book1 = new Book("1", "Java Programming", "John Smith", "978-0123456789", "Programming");
        Book book2 = new Book("2", "Python Guide", "Jane Doe", "978-0987654321", "Programming");
        Book book3 = new Book("3", "History of Art", "Bob Johnson", "978-0111111111", "Art");
        
        libraryService.addBook(book1);
        libraryService.addBook(book2);
        libraryService.addBook(book3);
        
        assertEquals(2, libraryService.searchBooks("Programming").size());
        assertEquals(1, libraryService.searchBooks("Java").size());
        assertEquals(1, libraryService.searchBooks("Jane").size());
    }
}