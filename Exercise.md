# Git 실습 시나리오 및 명령어 가이드

## 🎯 Chapter별 상세 실습 시나리오

### Chapter 1-2: Git 기본 워크플로우 실습

#### 시나리오 1: 첫 번째 프로젝트 시작하기
```bash
# 1. 프로젝트 폴더 생성 및 Git 초기화
mkdir hello-git-project
cd hello-git-project
git init

# 2. 첫 번째 파일 생성
echo "public class Hello {" > Hello.java
echo "    public static void main(String[] args) {" >> Hello.java
echo "        System.out.println(\"Hello Git!\");" >> Hello.java
echo "    }" >> Hello.java
echo "}" >> Hello.java

# 3. 첫 번째 커밋
git add Hello.java
git commit -m "Initial commit: Add Hello.java"

# 4. 파일 수정 후 두 번째 커밋
echo "        System.out.println(\"Git is awesome!\");" >> Hello.java
git add Hello.java
git commit -m "Add additional message to Hello.java"

# 5. 히스토리 확인
git log --oneline
git log --graph --decorate
```

#### 시나리오 2: .gitignore 설정하기
```bash
# 1. Java 프로젝트용 .gitignore 생성
cat > .gitignore << 'EOF'
# Compiled class files
*.class

# Log files
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# virtual machine crash logs
hs_err_pid*

# IDE files
.idea/
*.iml
.vscode/
.settings/
.project
.classpath

# OS generated files
.DS_Store
Thumbs.db
EOF

# 2. .gitignore 커밋
git add .gitignore
git commit -m "Add .gitignore for Java project"

# 3. 무시되는 파일 테스트
echo "public class Test {}" > Test.class
echo "Debug info" > debug.log
git status  # 무시된 파일들이 표시되지 않음을 확인
```

### Chapter 3: 브랜치 실습 시나리오

#### 시나리오 1: Feature 브랜치로 계산기 기능 추가
```bash
# 1. Calculator 프로젝트 시작
git checkout -b main  # main 브랜치로 이름 변경
# Calculator.java 기본 버전 생성 및 커밋

# 2. 고급 연산 기능 브랜치 생성
git checkout -b feature/advanced-operations
# power, sqrt 메서드 추가
git add Calculator.java
git commit -m "Add power and sqrt methods"

# 3. 메모리 기능 브랜치 생성 (main에서 분기)
git checkout main
git checkout -b feature/memory-functions
# memory 관련 메서드 추가
git add Calculator.java
git commit -m "Add memory store/recall/clear functions"

# 4. main에 고급 연산 기능 먼저 병합
git checkout main
git merge feature/advanced-operations
git branch -d feature/advanced-operations

# 5. 메모리 기능 병합 (충돌 발생 상황)
git merge feature/memory-functions
# 충돌 해결 후
git add Calculator.java
git commit -m "Merge memory functions (resolve conflicts)"
git branch -d feature/memory-functions
```

#### 시나리오 2: 충돌 해결 실습
```bash
# 1. 두 개의 브랜치에서 같은 부분 수정
git checkout -b feature/version-update
# Calculator.java의 VERSION을 "1.1.0"으로 변경
git add Calculator.java
git commit -m "Update version to 1.1.0"

git checkout main
# Calculator.java의 VERSION을 "1.0.1"로 변경
git add Calculator.java
git commit -m "Update version to 1.0.1"

# 2. 병합 시 충돌 발생
git merge feature/version-update
# 충돌 메시지 확인

# 3. 충돌 해결
# Calculator.java 파일을 열어 충돌 마커 확인
# <<<<<<< HEAD
#     private static final String VERSION = "1.0.1";
# =======
#     private static final String VERSION = "1.1.0";
# >>>>>>> feature/version-update

# 4. 수동으로 충돌 해결 (예: "1.1.0" 선택)
# 충돌 마커 제거 후 원하는 버전으로 수정

# 5. 충돌 해결 완료
git add Calculator.java
git commit -m "Resolve version conflict, keep 1.1.0"
```

### Chapter 4: GitHub 연동 실습

#### 시나리오 1: 로컬 프로젝트를 GitHub에 업로드
```bash
# 1. GitHub에서 새 저장소 생성 (웹에서)
# 저장소 이름: calculator-project

# 2. 로컬 저장소와 GitHub 연결
git remote add origin https://github.com/USERNAME/calculator-project.git
git branch -M main
git push -u origin main

# 3. 원격 저장소 확인
git remote -v
git branch -a

# 4. README 파일 추가
cat > README.md << 'EOF'
# Calculator Project

A simple calculator implementation in Java for learning Git.

## Features
- Basic arithmetic operations
- Advanced operations (power, square root)
- Memory functions

## How to Run
```bash
javac Calculator.java
java Calculator
```

## Git Learning Progress
- ✅ Basic Git commands
- ✅ Branching and merging
- ✅ GitHub integration
- 🔄 Team collaboration (in progress)
  EOF

git add README.md
git commit -m "Add README file"
git push origin main
```

#### 시나리오 2: 원격 저장소에서 협업
```bash
# 1. 다른 컴퓨터에서 저장소 클론 (팀원 역할)
git clone https://github.com/USERNAME/calculator-project.git
cd calculator-project

# 2. 새로운 기능 브랜치 생성
git checkout -b feature/input-validation
# 입력값 검증 기능 추가
git add .
git commit -m "Add input validation for calculator operations"
git push origin feature/input-validation

# 3. GitHub에서 Pull Request 생성 (웹에서)
# - feature/input-validation → main
# - 코드 리뷰 요청

# 4. 원본 저장소에서 변경사항 가져오기
git checkout main
git pull origin main
```

### Chapter 5: 팀 협업 워크플로우

#### 시나리오 1: 사용자 관리 시스템 팀 개발
```bash
# 팀장 역할: 프로젝트 초기 설정
mkdir user-management-system
cd user-management-system
git init
git checkout -b main

# User.java 기본 클래스 생성
git add User.java
git commit -m "Add User entity class"

# GitHub 저장소 생성 후 푸시
git remote add origin https://github.com/TEAM/user-management-system.git
git push -u origin main

# 팀원 1: 사용자 서비스 개발
git clone https://github.com/TEAM/user-management-system.git
cd user-management-system
git checkout -b feature/user-service

# UserService.java 개발
git add UserService.java
git commit -m "Implement UserService with registration and login"
git push origin feature/user-service

# 팀원 2: 인증 서비스 개발 (동시 작업)
git checkout main
git pull origin main
git checkout -b feature/authentication

# AuthenticationService.java 개발
git add AuthenticationService.java
git commit -m "Implement AuthenticationService with session management"
git push origin feature/authentication

# 팀장: 첫 번째 PR 리뷰 및 머지
# GitHub에서 feature/user-service → main PR 머지

# 팀원 2: main 브랜치 동기화 후 작업 계속
git checkout main
git pull origin main
git checkout feature/authentication
git rebase main  # 또는 git merge main
# 충돌 해결 (필요한 경우)
git push origin feature/authentication --force-with-lease
```

#### 시나리오 2: 코드 리뷰 프로세스
```bash
# 1. PR 생성 전 체크리스트
git checkout feature/authentication
# 코드 품질 검사
javac *.java  # 컴파일 에러 확인
# 테스트 실행 (만약 테스트가 있다면)
git log --oneline  # 커밋 메시지 확인

# 2. PR 생성 후 피드백 반영
# GitHub에서 리뷰어가 댓글 작성

# 3. 피드백 반영
# 코드 수정
git add AuthenticationService.java
git commit -m "Fix session timeout logic based on code review"
git push origin feature/authentication

# 4. 리뷰어 재검토 후 승인
# GitHub에서 "Approve" 후 머지
```

### Chapter 6: 고급 Git 명령어 실습

#### 시나리오 1: 커밋 수정과 히스토리 정리
```bash
# 1. 마지막 커밋 메시지 수정
git commit --amend -m "Fix typo in authentication service implementation"

# 2. 여러 커밋을 하나로 합치기 (Squash)
git log --oneline  # 최근 3개 커밋 확인
git rebase -i HEAD~3

# 편집기에서:
# pick abc1234 Add authentication service
# squash def5678 Fix authentication bug
# squash ghi9012 Update documentation
# 저장 후 종료

# 3. 특정 커밋의 변경사항만 적용 (Cherry-pick)
git checkout main
git log --oneline feature/experimental-feature  # 원하는 커밋 해시 확인
git cherry-pick abc1234

# 4. 작업 중인 변경사항 임시 저장
git stash push -m "Work in progress on user validation"
git checkout other-branch
# 다른 작업 수행
git checkout feature/user-validation
git stash pop
```

#### 시나리오 2: 실수 복구하기
```bash
# 1. 잘못된 파일 추가 취소
git add wrong-file.txt
git status
git reset HEAD wrong-file.txt

# 2. 마지막 커밋 취소 (변경사항 유지)
git reset --soft HEAD~1
git status  # 변경사항이 스테이징 영역에 있음

# 3. 마지막 커밋 완전히 취소 (변경사항 삭제)
git reset --hard HEAD~1
# 주의: 변경사항이 완전히 사라짐

# 4. 삭제된 커밋 복구
git reflog  # 삭제된 커밋 해시 찾기
git checkout abc1234  # 삭제된 커밋으로 이동
git checkout -b recover-deleted-work  # 새 브랜치 생성

# 5. 특정 파일의 변경사항 되돌리기
git restore filename.java  # 워킹 디렉토리의 변경사항 취소
git restore --staged filename.java  # 스테이징된 변경사항 취소
```

### Chapter 7: 실무 시나리오 실습

#### 시나리오 1: 긴급 버그 수정 (Hotfix)
```bash
# 상황: 프로덕션에서 중요한 버그 발견
# 현재 개발 중인 기능이 있지만 긴급 수정 필요

# 1. 현재 작업 임시 저장
git stash push -m "WIP: new feature development"

# 2. 프로덕션 버전에서 hotfix 브랜치 생성
git checkout main
git pull origin main
git checkout -b hotfix/critical-security-fix

# 3. 버그 수정
# UserService.java에서 보안 취약점 수정
git add UserService.java
git commit -m "Fix critical security vulnerability in password validation"

# 4. 테스트 후 main에 즉시 머지
git checkout main
git merge hotfix/critical-security-fix
git push origin main

# 5. 개발 브랜치에도 적용
git checkout develop  # 또는 현재 개발 브랜치
git merge hotfix/critical-security-fix

# 6. 이전 작업 복원
git stash pop

# 7. hotfix 브랜치 정리
git branch -d hotfix/critical-security-fix
git push origin --delete hotfix/critical-security-fix
```

#### 시나리오 2: 대용량 기능 개발 관리
```bash
# 상황: 도서관 관리 시스템의 대규모 기능 개발 (2-3주 소요 예상)

# 1. 장기 기능 브랜치 생성
git checkout -b feature/library-system
git push -u origin feature/library-system

# 2. 기능을 세부 작업으로 나누어 개발
git checkout -b feature/library-system/book-management
# Book.java, BookService.java 개발
git add .
git commit -m "Implement book management functionality"
git push origin feature/library-system/book-management

# 3. 세부 기능을 메인 기능 브랜치에 머지
git checkout feature/library-system
git merge feature/library-system/book-management
git branch -d feature/library-system/book-management

# 4. 정기적으로 main 브랜치와 동기화 (주 1-2회)
git checkout main
git pull origin main
git checkout feature/library-system
git merge main
# 충돌 해결 (필요한 경우)
git push origin feature/library-system

# 5. 다음 세부 기능 개발
git checkout -b feature/library-system/borrow-management
# BorrowRecord.java, 대출 기능 개발
git add .
git commit -m "Implement book borrowing and returning"
git push origin feature/library-system/borrow-management

# 6. 모든 기능 완료 후 main에 머지
git checkout feature/library-system
git merge feature/library-system/borrow-management
git checkout main
git pull origin main
git merge feature/library-system
git push origin main
```

#### 시나리오 3: 릴리즈 관리
```bash
# 상황: v1.0.0 릴리즈 준비

# 1. 릴리즈 브랜치 생성
git checkout main
git pull origin main
git checkout -b release/v1.0.0

# 2. 버전 정보 업데이트
# version.properties 파일 생성
echo "version=1.0.0" > version.properties
echo "build.date=$(date)" >> version.properties
git add version.properties
git commit -m "Prepare release v1.0.0"

# 3. 릴리즈 노트 작성
cat > RELEASE_NOTES.md << 'EOF'
# Release Notes v1.0.0

## New Features
- User management system
- Authentication with session management
- Library book management
- Book borrowing and returning system

## Bug Fixes
- Fixed password validation security issue
- Improved error handling in user registration

## Breaking Changes
- None

## Migration Guide
- No migration needed for new installation
EOF

git add RELEASE_NOTES.md
git commit -m "Add release notes for v1.0.0"

# 4. 릴리즈 테스트 및 버그 수정
# 테스트 중 발견된 버그 수정
git add .
git commit -m "Fix minor bug in book search functionality"

# 5. main에 머지 및 태그 생성
git checkout main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0

# 6. develop 브랜치에도 반영 (Git Flow 방식 사용 시)
git checkout develop
git merge release/v1.0.0
git push origin develop

# 7. 릴리즈 브랜치 정리
git branch -d release/v1.0.0
git push origin --delete release/v1.0.0
```

### Chapter 8: GitHub 고급 기능 실습

#### 시나리오 1: GitHub Actions를 활용한 CI/CD
```yaml
# .github/workflows/ci.yml 파일 생성
name: Java CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'temurin'
        
    - name: Compile Java code
      run: |
        javac *.java
        
    - name: Run tests
      run: |
        # JUnit 테스트 실행 (만약 있다면)
        echo "Running tests..."
        
    - name: Create JAR
      run: |
        jar cf library-system.jar *.class
        
    - name: Upload JAR artifact
      uses: actions/upload-artifact@v3
      with:
        name: library-system-jar
        path: library-system.jar
```

#### 시나리오 2: 이슈 및 프로젝트 보드 활용
```bash
# 1. GitHub Issues 생성 (웹에서)
# 제목: "Add user profile management feature"
# 레이블: enhancement, priority-high
# 마일스톤: v1.1.0

# 2. 이슈와 연결된 브랜치 생성
git checkout -b feature/user-profile-management

# 3. 커밋에 이슈 번호 포함
git commit -m "Add user profile entity class

Implements basic user profile structure for issue #123"

# 4. PR에서 이슈 자동 닫기
# PR 설명에 "Closes #123" 포함

# 5. GitHub Projects 보드에서 진행 상황 추적
# To Do → In Progress → Review → Done
```

## 🔧 실습용 스크립트 및 도구

### 자동 설정 스크립트
```bash
#!/bin/bash
# setup-git-environment.sh

# Git 전역 설정
echo "Setting up Git configuration..."
read -p "Enter your name: " name
read -p "Enter your email: " email

git config --global user.name "$name"
git config --global user.email "$email"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"  # VS Code 사용 시

# 유용한 Git 별칭 설정
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"

# 컬러 출력 활성화
git config --global color.ui auto

echo "Git configuration completed!"
git config --list --global
```

### 실습 환경 체크 스크립트
```bash
#!/bin/bash
# check-environment.sh

echo "=== Git Environment Check ==="

# Git 버전 확인
echo "Git version:"
git --version

# Git 설정 확인
echo -e "\nGit configuration:"
echo "Name: $(git config user.name)"
echo "Email: $(git config user.email)"
echo "Default branch: $(git config init.defaultBranch)"

# Java 환경 확인
echo -e "\nJava version:"
java -version

echo -e "\nJavac version:"
javac -version

# GitHub CLI 설치 확인 (선택사항)
if command -v gh &> /dev/null; then
    echo -e "\nGitHub CLI version:"
    gh --version
else
    echo -e "\nGitHub CLI not installed (optional)"
fi

echo -e "\n=== Environment Check Complete ==="
```

### 프로젝트 템플릿 생성 스크립트
```bash
#!/bin/bash
# create-project-template.sh

read -p "Enter project name: " project_name
mkdir "$project_name"
cd "$project_name"

# Git 초기화
git init
git checkout -b main

# .gitignore 생성
cat > .gitignore << 'EOF'
*.class
*.log
*.ctxt
.mtj.tmp/
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar
hs_err_pid*
.idea/
*.iml
.vscode/
.settings/
.project
.classpath
.DS_Store
Thumbs.db
EOF

# README.md 생성
cat > README.md << EOF
# $project_name

## Description
[Project description here]

## How to Run
\`\`\`bash
javac *.java
java Main
\`\`\`

## Git Learning Progress
- [ ] Basic Git commands
- [ ] Branching and merging
- [ ] GitHub integration
- [ ] Team collaboration
EOF

# 기본 Java 파일 생성
cat > Main.java << EOF
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, $project_name!");
    }
}
EOF

# 첫 커밋
git add .
git commit -m "Initial commit: Project setup"

echo "Project '$project_name' created successfully!"
echo "Next steps:"
echo "1. cd $project_name"
echo "2. Start coding!"
echo "3. Create GitHub repository and push"
```

## 📚 추가 학습 자료

### Git 명령어 치트 시트
```bash
# 기본 명령어
git init                    # 저장소 초기화
git clone <url>            # 저장소 복제
git status                 # 상태 확인
git add <file>             # 파일 스테이징
git add .                  # 모든 변경사항 스테이징
git commit -m "message"    # 커밋
git push                   # 원격 저장소에 푸시
git pull                   # 원격 저장소에서 풀

# 브랜치 관리
git branch                 # 브랜치 목록
git branch <name>          # 브랜치 생성
git checkout <branch>      # 브랜치 전환
git checkout -b <branch>   # 브랜치 생성 및 전환
git merge <branch>         # 브랜치 병합
git branch -d <branch>     # 브랜치 삭제

# 히스토리 확인
git log                    # 커밋 히스토리
git log --oneline          # 간단한 히스토리
git log --graph            # 그래프 형태로 히스토리
git diff                   # 변경사항 확인
git diff --staged          # 스테이징된 변경사항 확인

# 실수 복구
git reset HEAD <file>      # 스테이징 취소
git restore <file>         # 파일 복원
git reset --soft HEAD~1    # 마지막 커밋 취소 (변경사항 유지)
git reset --hard HEAD~1    # 마지막 커밋 취소 (변경사항 삭제)
git revert <commit>        # 커밋 되돌리기

# 고급 명령어
git stash                  # 변경사항 임시 저장
git stash pop              # 임시 저장된 변경사항 복원
git cherry-pick <commit>   # 특정 커밋 적용
git rebase -i HEAD~3       # 대화형 리베이스
git reflog                 # 참조 로그 확인
```

### 좋은 커밋 메시지 작성법
```
타입(범위): 간단한 설명

상세한 설명 (필요한 경우)

- 변경사항 1
- 변경사항 2

Closes #123, #456
```

**타입 예시:**
- `feat`: 새로운 기능
- `fix`: 버그 수정
- `docs`: 문서 변경
- `style`: 코드 스타일 변경
- `refactor`: 리팩토링
- `test`: 테스트 추가/수정
- `chore`: 빌드 프로세스나 도구 변경

### 팀 협업 베스트 프랙티스

1. **브랜치 명명 규칙**
    - `feature/기능명`
    - `bugfix/버그명`
    - `hotfix/긴급수정명`
    - `release/버전명`

2. **PR 작성 가이드라인**
    - 명확한 제목과 설명
    - 변경사항 요약
    - 테스트 결과
    - 관련 이슈 번호

3. **코드 리뷰 체크포인트**
    - 코드 품질
    - 테스트 커버리지
    - 문서화
    - 보안 고려사항

이 가이드를 통해 실제 업무에서 발생할 수 있는 다양한 Git 시나리오를 경험하고, 팀 협업에 필요한 Git 워크플로우를 완전히 습득할 수 있습니다.