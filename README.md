# Git/GitHub A to Z 세미나 커리큘럼

## 📋 세미나 개요
- **대상**: Git 초보자 (SVN 사용 경험자 포함)
- **목표**: Git/GitHub를 활용한 실무 개발 프로세스 완전 습득
- **방식**: 실습 중심 (이론 30% + 실습 70%)
- **총 소요시간**: 약 16-20시간 (4일 과정, 일일 4-5시간)

## 📚 챕터별 상세 커리큘럼

### 🎯 Chapter 1: Git 기본 개념과 설치 (2시간)

#### 학습 목표
- Git의 기본 개념 이해
- SVN과 Git의 차이점 파악
- Git 환경 설정 완료

#### 이론 내용 (30분)
1. **버전 관리 시스템이란?**
    - 중앙 집중식 vs 분산 버전 관리
    - SVN vs Git 비교표

2. **Git의 핵심 개념**
    - Working Directory, Staging Area, Repository
    - Commit, Branch, Merge의 개념

#### 과정 링ㅋ 
- [소스코드](./SourceCode.md)
- [실습](./Exercise.md)
- [강사가이드](./Guide.md)

#### 실습 내용 (1시간 30분)
1. **Git 설치 및 초기 설정**
   ```bash
   # Git 설치 확인
   git --version
   
   # 사용자 정보 설정
   git config --global user.name "홍길동"
   git config --global user.email "hong@company.com"
   
   # 설정 확인
   git config --list
   ```

2. **첫 번째 Git 저장소 만들기**
   ```bash
   # 프로젝트 폴더 생성
   mkdir my-first-git-project
   cd my-first-git-project
   
   # Git 저장소 초기화
   git init
   
   # 상태 확인
   git status
   ```

#### 실습 프로젝트
- 간단한 "Hello Git" 텍스트 파일 생성 및 첫 커밋

---

### 🎯 Chapter 2: 기본 Git 명령어와 워크플로우 (3시간)

#### 학습 목표
- Git의 기본 명령어 완전 습득
- 파일 생명주기 이해
- 커밋 히스토리 관리

#### 이론 내용 (45분)
1. **파일의 상태 변화**
    - Untracked → Staged → Committed
    - Modified 상태의 이해

2. **Git 명령어 체계**
    - add, commit, status, log, diff
    - 각 명령어의 옵션들

#### 실습 내용 (2시간 15분)
1. **기본 Git 워크플로우**
   ```bash
   # 파일 생성 및 추가
   echo "Hello Git World" > hello.txt
   git add hello.txt
   git commit -m "Add hello.txt file"
   
   # 파일 수정 후 재커밋
   echo "Git is awesome!" >> hello.txt
   git add hello.txt
   git commit -m "Update hello.txt with additional message"
   
   # 히스토리 확인
   git log
   git log --oneline
   git log --graph
   ```

2. **파일 상태 관리**
   ```bash
   # 여러 파일 한번에 추가
   git add .
   git add *.java
   
   # 스테이징 취소
   git reset HEAD filename
   
   # 변경사항 확인
   git diff
   git diff --staged
   ```

#### 실습 프로젝트 (Java)
간단한 Calculator 클래스 개발을 통한 Git 기본 워크플로우 실습

---

### 🎯 Chapter 3: 브랜치와 병합 (3시간)

#### 학습 목표
- 브랜치 개념 완전 이해
- 브랜치 생성, 전환, 병합 실습
- 충돌 해결 방법 습득

#### 이론 내용 (45분)
1. **브랜치란 무엇인가?**
    - SVN의 브랜치 vs Git의 브랜치
    - Git 브랜치의 가벼움

2. **브랜치 전략**
    - Feature Branch 전략
    - Git Flow 소개

#### 실습 내용 (2시간 15분)
1. **브랜치 기본 조작**
   ```bash
   # 브랜치 생성 및 전환
   git branch feature-login
   git checkout feature-login
   # 또는
   git checkout -b feature-signup
   
   # 브랜치 목록 확인
   git branch
   git branch -a
   
   # 브랜치 삭제
   git branch -d feature-name
   ```

2. **브랜치 병합과 충돌 해결**
   ```bash
   # Fast-forward 병합
   git checkout main
   git merge feature-login
   
   # 3-way 병합
   git merge feature-signup
   
   # 충돌 발생 시 해결 과정
   # 1. 충돌 파일 수정
   # 2. git add 충돌파일
   # 3. git commit
   ```

#### 실습 프로젝트 (Java)
사용자 관리 시스템의 로그인/회원가입 기능을 각각 다른 브랜치에서 개발 후 병합

---

### 🎯 Chapter 4: GitHub 시작하기 (2시간)

#### 학습 목표
- GitHub 계정 생성 및 저장소 생성
- 로컬과 원격 저장소 연결
- Push/Pull 개념 이해

#### 이론 내용 (30분)
1. **GitHub란?**
    - Git 호스팅 서비스
    - 협업 도구로서의 GitHub

2. **원격 저장소 개념**
    - origin의 의미
    - upstream과 downstream

#### 실습 내용 (1시간 30분)
1. **GitHub 저장소 생성 및 연결**
   ```bash
   # 원격 저장소 추가
   git remote add origin https://github.com/username/repo.git
   
   # 원격 저장소에 푸시
   git push -u origin main
   
   # 원격 저장소 정보 확인
   git remote -v
   ```

2. **원격 저장소와의 동기화**
   ```bash
   # 원격 저장소에서 가져오기
   git pull origin main
   
   # 또는 fetch 후 merge
   git fetch origin
   git merge origin/main
   ```

#### 실습 프로젝트
로컬에서 개발한 Calculator 프로젝트를 GitHub에 업로드

---

### 🎯 Chapter 5: 협업 워크플로우 (4시간)

#### 학습 목표
- 팀 협업을 위한 Git 워크플로우 이해
- Pull Request/Merge Request 과정 습득
- 코드 리뷰 프로세스 경험

#### 이론 내용 (1시간)
1. **협업 워크플로우 전략**
    - Centralized Workflow
    - Feature Branch Workflow
    - Gitflow Workflow
    - Forking Workflow

2. **Pull Request 프로세스**
    - PR의 목적과 장점
    - 코드 리뷰의 중요성

#### 실습 내용 (3시간)
1. **팀 프로젝트 시뮬레이션**
   ```bash
   # Feature 브랜치에서 작업
   git checkout -b feature/user-authentication
   # 개발 작업 수행
   git add .
   git commit -m "Implement user authentication"
   git push origin feature/user-authentication
   ```

2. **Pull Request 생성 및 리뷰**
    - GitHub에서 PR 생성
    - 코드 리뷰 및 피드백
    - 수정 후 재푸시
    - PR 머지

3. **충돌 해결 실습**
    - 의도적으로 충돌 상황 생성
    - 충돌 해결 프로세스 실습

#### 실습 프로젝트 (Java)
간단한 도서관 관리 시스템을 여러 명이 나누어 개발 (사용자 관리, 도서 관리, 대출 관리 등)

---

### 🎯 Chapter 6: 고급 Git 명령어 (2시간)

#### 학습 목표
- 실무에서 자주 사용하는 고급 명령어 습득
- 실수 복구 방법 학습
- Git 히스토리 관리

#### 이론 내용 (30분)
1. **Git 내부 구조 간단히**
    - HEAD, refs, objects
    - Commit의 실체

2. **실무에서의 Git 사용법**
    - 좋은 커밋 메시지 작성법
    - .gitignore 활용법

#### 실습 내용 (1시간 30분)
1. **유용한 Git 명령어들**
   ```bash
   # 커밋 수정
   git commit --amend
   
   # 특정 커밋으로 이동
   git checkout commit-hash
   git checkout HEAD~3
   
   # 변경사항 임시 저장
   git stash
   git stash pop
   git stash list
   
   # 파일 복원
   git restore filename
   git restore --staged filename
   
   # 히스토리 정리
   git rebase -i HEAD~3
   
   # 특정 커밋 선택적 적용
   git cherry-pick commit-hash
   ```

2. **실수 복구하기**
   ```bash
   # 커밋 되돌리기
   git revert HEAD
   git reset --soft HEAD~1
   git reset --hard HEAD~1
   
   # 분실된 커밋 찾기
   git reflog
   ```

#### 실습 프로젝트
기존 프로젝트에서 다양한 상황별 Git 명령어 실습

---

### 🎯 Chapter 7: 실무 시나리오 실습 (3시간)

#### 학습 목표
- 실제 개발 환경에서 발생할 수 있는 다양한 상황 해결
- 팀 협업 프로세스 완전 체화
- 트러블슈팅 능력 향상

#### 실습 시나리오들 (3시간)
1. **긴급 버그 수정 시나리오** (45분)
    - Hotfix 브랜치 생성
    - 빠른 수정 후 배포
    - 여러 브랜치에 적용

2. **대용량 기능 개발 시나리오** (1시간)
    - 장기간 브랜치 관리
    - 정기적인 메인 브랜치 동기화
    - Feature 브랜치 세분화

3. **팀원 퇴사 시 브랜치 정리** (30분)
    - 미완성 작업 파악
    - 브랜치 정리 및 이관

4. **릴리즈 관리 시나리오** (45분)
    - Release 브랜치 생성
    - 태그 생성 및 관리
    - 버전 관리 전략

#### 실습 프로젝트 (Java)
완전한 웹 애플리케이션 (Spring Boot 기반 간단한 게시판) 팀 개발

---

### 🎯 Chapter 8: GitHub 고급 기능과 도구들 (1시간)

#### 학습 목표
- GitHub의 협업 도구들 활용
- 프로젝트 관리 기능 이해
- 자동화 도구 소개

#### 이론 및 실습 내용 (1시간)
1. **GitHub 협업 도구**
    - Issues 활용법
    - Projects 보드 사용
    - Wiki 작성

2. **GitHub Actions 소개**
    - CI/CD 기본 개념
    - 간단한 자동화 설정

3. **보안 및 권한 관리**
    - 브랜치 보호 규칙
    - 팀 권한 설정
    - 코드 리뷰 필수화

---

## 📁 실습 프로젝트 상세

### 프로젝트 1: Hello Git (Chapter 1-2)
```java
// Hello.java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Git!");
        System.out.println("Learning Git is fun!");
    }
}
```

### 프로젝트 2: Calculator (Chapter 2-4)
```java
// Calculator.java
public class Calculator {
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
            throw new IllegalArgumentException("Division by zero");
        }
        return (double) a / b;
    }
}
```

```java
// CalculatorTest.java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    private Calculator calculator = new Calculator();
    
    @Test
    public void testAdd() {
        assertEquals(5, calculator.add(2, 3));
    }
    
    @Test
    public void testSubtract() {
        assertEquals(1, calculator.subtract(3, 2));
    }
    
    @Test
    public void testMultiply() {
        assertEquals(6, calculator.multiply(2, 3));
    }
    
    @Test
    public void testDivide() {
        assertEquals(2.0, calculator.divide(4, 2), 0.001);
    }
    
    @Test
    public void testDivideByZero() {
        assertThrows(IllegalArgumentException.class, 
                    () -> calculator.divide(1, 0));
    }
}
```

### 프로젝트 3: 사용자 관리 시스템 (Chapter 3, 5)
```java
// User.java
public class User {
    private String username;
    private String email;
    private String password;
    
    public User(String username, String email, String password) {
        this.username = username;
        this.email = email;
        this.password = password;
    }
    
    // getters and setters
    public String getUsername() { return username; }
    public void setUsername(String username) { this.username = username; }
    
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
    
    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }
}
```

```java
// UserService.java
import java.util.*;

public class UserService {
    private Map<String, User> users = new HashMap<>();
    
    public boolean register(User user) {
        if (users.containsKey(user.getUsername())) {
            return false;
        }
        users.put(user.getUsername(), user);
        return true;
    }
    
    public boolean login(String username, String password) {
        User user = users.get(username);
        return user != null && user.getPassword().equals(password);
    }
    
    public User findUser(String username) {
        return users.get(username);
    }
}
```

### 프로젝트 4: 도서관 관리 시스템 (Chapter 5, 7)
```java
// Book.java
public class Book {
    private String id;
    private String title;
    private String author;
    private boolean available;
    
    public Book(String id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.available = true;
    }
    
    // getters and setters
    public String getId() { return id; }
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
    public boolean isAvailable() { return available; }
    public void setAvailable(boolean available) { this.available = available; }
}
```

```java
// LibraryService.java
import java.util.*;

public class LibraryService {
    private Map<String, Book> books = new HashMap<>();
    private Map<String, Set<String>> userBorrowedBooks = new HashMap<>();
    
    public void addBook(Book book) {
        books.put(book.getId(), book);
    }
    
    public boolean borrowBook(String userId, String bookId) {
        Book book = books.get(bookId);
        if (book != null && book.isAvailable()) {
            book.setAvailable(false);
            userBorrowedBooks.computeIfAbsent(userId, k -> new HashSet<>())
                            .add(bookId);
            return true;
        }
        return false;
    }
    
    public boolean returnBook(String userId, String bookId) {
        Set<String> borrowed = userBorrowedBooks.get(userId);
        if (borrowed != null && borrowed.contains(bookId)) {
            books.get(bookId).setAvailable(true);
            borrowed.remove(bookId);
            return true;
        }
        return false;
    }
    
    public List<Book> getAvailableBooks() {
        return books.values().stream()
                   .filter(Book::isAvailable)
                   .collect(ArrayList::new, ArrayList::add, ArrayList::addAll);
    }
}
```

## 🎯 세미나 진행 방식

### 사전 준비사항
1. **필요 도구 설치**
    - Git (최신 버전)
    - IntelliJ IDEA 또는 Eclipse
    - GitHub 계정 생성

2. **실습 환경 세팅**
    - Java 11 이상
    - JUnit 5
    - 각자의 GitHub 저장소

### 각 챕터별 진행 방식
1. **이론 설명** (20-30분)
    - 개념 소개 및 SVN과의 비교
    - 실무 활용 사례 공유

2. **단계별 실습** (60-120분)
    - 강사 시연 → 따라하기 → 개별 실습
    - 실습 중 궁금한 점 즉시 질의응답

3. **마무리** (10-20분)
    - 핵심 내용 요약
    - 다음 챕터 예고
    - 과제 안내

### 평가 및 피드백
- 각 챕터별 실습 완료도 체크
- 마지막 날 팀 프로젝트 발표
- 개인별 Git/GitHub 활용도 평가

## 📖 참고 자료
- [Git 공식 문서](https://git-scm.com/doc)
- [GitHub 학습 자료](https://github.com/skills)
- [Atlassian Git 튜토리얼](https://www.atlassian.com/git/tutorials)

## 🚀 세미나 후 실무 적용 계획
1. **1주차**: 개인 프로젝트로 Git 워크플로우 연습
2. **2주차**: 소규모 팀 프로젝트 진행
3. **3주차**: 전사 Git/GitHub 전환 시작
4. **4주차**: 피드백 수집 및 프로세스 개선
