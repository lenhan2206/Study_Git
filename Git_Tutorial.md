# Hướng Dẫn Học Git - Từ Cơ Bản Đến Nâng Cao

> Tài liệu học Git dựa trên khóa học từ [Fullstack.edu.vn](https://fullstack.edu.vn/learning/git?id=d65573db-7d77-4753-83fa-c2f51baabb5d)

## Mục Lục
1. [Giới thiệu về Git](#giới-thiệu-về-git)
2. [Cài đặt và Cấu hình](#cài-đặt-và-cấu-hình)
3. [Khởi tạo Repository](#khởi-tạo-repository)
4. [Các thao tác cơ bản](#các-thao-tác-cơ-bản)
5. [Làm việc với Branch](#làm-việc-với-branch)
6. [Remote Repository](#remote-repository)
7. [Giải quyết xung đột](#giải-quyết-xung-đột)
8. [Các lệnh nâng cao](#các-lệnh-nâng-cao)
9. [Best Practices](#best-practices)
10. [Tài nguyên học tập](#tài-nguyên-học-tập)

---

## Giới thiệu về Git

### Git là gì?
Git là một **hệ thống quản lý phiên bản phân tán** (Distributed Version Control System) được phát triển bởi Linus Torvalds vào năm 2005. Git giúp:

- **Theo dõi thay đổi**: Ghi lại mọi thay đổi trong code
- **Làm việc nhóm**: Nhiều người có thể cùng làm việc trên một dự án
- **Khôi phục**: Quay lại bất kỳ phiên bản nào trước đó
- **Phân nhánh**: Tạo các nhánh để phát triển tính năng mới

### Tại sao cần Git?
- **Backup**: Không bao giờ mất code
- **Collaboration**: Làm việc nhóm hiệu quả
- **History**: Theo dõi lịch sử phát triển
- **Rollback**: Quay lại phiên bản ổn định khi có lỗi

---

## Cài đặt và Cấu hình

### 1. Cài đặt Git

#### Windows
```bash
# Tải từ https://git-scm.com/download/win
# Hoặc sử dụng Chocolatey
choco install git

# Hoặc sử dụng winget
winget install Git.Git
```

#### macOS
```bash
# Sử dụng Homebrew
brew install git

# Hoặc tải từ https://git-scm.com/download/mac
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### 2. Cấu hình Git

#### Cấu hình cơ bản
```bash
# Cấu hình tên người dùng
git config --global user.name "Tên Của Bạn"

# Cấu hình email
git config --global user.email "email@example.com"

# Kiểm tra cấu hình
git config --list
```

#### Cấu hình nâng cao
```bash
# Đặt editor mặc định
git config --global core.editor "code --wait"

# Đặt branch mặc định
git config --global init.defaultBranch main

# Cấu hình line ending (Windows)
git config --global core.autocrlf true

# Cấu hình line ending (macOS/Linux)
git config --global core.autocrlf input
```

---

## Khởi tạo Repository

### 1. Tạo Repository mới

```bash
# Tạo thư mục dự án
mkdir my-project
cd my-project

# Khởi tạo Git repository
git init

# Kiểm tra trạng thái
git status
```

### 2. Clone Repository có sẵn

```bash
# Clone từ GitHub/GitLab
git clone https://github.com/username/repository.git

# Clone với tên thư mục tùy chỉnh
git clone https://github.com/username/repository.git my-folder

# Clone chỉ nhánh cụ thể
git clone -b branch-name https://github.com/username/repository.git
```

---

## Các thao tác cơ bản

### 1. Workflow cơ bản

```bash
# 1. Kiểm tra trạng thái
git status

# 2. Thêm file vào staging area
git add filename.txt
git add .                    # Thêm tất cả file
git add *.js                 # Thêm tất cả file .js

# 3. Commit thay đổi
git commit -m "Thông điệp commit"

# 4. Xem lịch sử
git log
```

### 2. Các lệnh quan trọng

#### Kiểm tra trạng thái
```bash
git status                  # Trạng thái tổng quan
git status --short          # Trạng thái ngắn gọn
git diff                    # Xem thay đổi chưa staged
git diff --staged           # Xem thay đổi đã staged
```

#### Thêm file
```bash
git add file.txt            # Thêm file cụ thể
git add .                   # Thêm tất cả
git add -A                  # Thêm tất cả (bao gồm file đã xóa)
git add -u                  # Chỉ thêm file đã được track
```

#### Commit
```bash
git commit -m "Message"     # Commit với message
git commit -am "Message"    # Add và commit cùng lúc
git commit --amend          # Sửa commit cuối cùng
```

#### Xem lịch sử
```bash
git log                     # Lịch sử đầy đủ
git log --oneline           # Lịch sử ngắn gọn
git log --graph             # Lịch sử với biểu đồ
git log --author="Name"     # Lọc theo tác giả
```

### 3. Undo và Reset

```bash
# Undo thay đổi chưa staged
git checkout -- filename.txt
git restore filename.txt

# Undo thay đổi đã staged
git reset HEAD filename.txt
git restore --staged filename.txt

# Undo commit (giữ thay đổi)
git reset --soft HEAD~1

# Undo commit (xóa thay đổi)
git reset --hard HEAD~1
```

---

## Làm việc với Branch

### 1. Tạo và chuyển đổi Branch

```bash
# Tạo branch mới
git branch feature-branch

# Chuyển sang branch
git checkout feature-branch
git switch feature-branch

# Tạo và chuyển sang branch mới
git checkout -b feature-branch
git switch -c feature-branch

# Xem danh sách branch
git branch                  # Local branches
git branch -r               # Remote branches
git branch -a               # Tất cả branches
```

### 2. Merge Branch

```bash
# Chuyển về branch chính
git checkout main

# Merge branch
git merge feature-branch

# Merge với no-fast-forward
git merge --no-ff feature-branch

# Xóa branch đã merge
git branch -d feature-branch
```

### 3. Rebase

```bash
# Rebase branch hiện tại lên main
git rebase main

# Interactive rebase
git rebase -i HEAD~3

# Abort rebase
git rebase --abort
```

---

## Remote Repository

### 1. Thêm Remote

```bash
# Thêm remote origin
git remote add origin https://github.com/username/repo.git

# Xem danh sách remote
git remote -v

# Thay đổi URL remote
git remote set-url origin new-url
```

### 2. Push và Pull

```bash
# Push lần đầu
git push -u origin main

# Push thông thường
git push origin main
git push origin feature-branch

# Pull thay đổi
git pull origin main

# Fetch thay đổi (không merge)
git fetch origin
```

### 3. Fork và Pull Request

```bash
# Fork repository trên GitHub
# Clone fork về máy
git clone https://github.com/your-username/forked-repo.git

# Thêm upstream
git remote add upstream https://github.com/original-owner/repo.git

# Sync với upstream
git fetch upstream
git checkout main
git merge upstream/main
```

---

## Giải quyết xung đột

### 1. Khi nào xảy ra xung đột?
- Hai người cùng sửa một dòng code
- Merge hai branch có thay đổi cùng file
- Rebase có xung đột

### 2. Cách giải quyết

```bash
# 1. Git sẽ báo xung đột
git merge feature-branch

# 2. Mở file bị xung đột
# Tìm các marker:
# <<<<<<< HEAD
# Code từ branch hiện tại
# =======
# Code từ branch merge
# >>>>>>> feature-branch

# 3. Chỉnh sửa file, xóa markers
# 4. Add file đã sửa
git add filename.txt

# 5. Commit
git commit -m "Resolve merge conflict"
```

### 3. Công cụ hỗ trợ

```bash
# Sử dụng merge tool
git mergetool

# Cấu hình merge tool
git config --global merge.tool vscode
```

---

## Các lệnh nâng cao

### 1. Stash

```bash
# Lưu thay đổi tạm thời
git stash
git stash save "Message"

# Xem danh sách stash
git stash list

# Áp dụng stash
git stash apply
git stash pop

# Xóa stash
git stash drop
git stash clear
```

### 2. Cherry-pick

```bash
# Lấy commit từ branch khác
git cherry-pick commit-hash

# Cherry-pick nhiều commit
git cherry-pick commit1 commit2
```

### 3. Tag

```bash
# Tạo tag
git tag v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tag
git push origin v1.0.0
git push origin --tags

# Xóa tag
git tag -d v1.0.0
git push origin --delete v1.0.0
```

### 4. Submodule

```bash
# Thêm submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Clone repository có submodule
git clone --recursive https://github.com/user/repo.git

# Update submodule
git submodule update --remote
```

---

## Best Practices

### 1. Commit Message

```bash
# Format chuẩn
type(scope): description

# Ví dụ
feat(auth): add login functionality
fix(ui): resolve button alignment issue
docs(readme): update installation guide
refactor(api): simplify user service
test(auth): add unit tests for login
```

### 2. Branch Naming

```bash
# Feature branch
feature/user-authentication
feature/payment-integration

# Bug fix branch
bugfix/login-error
hotfix/security-patch

# Release branch
release/v1.2.0
```

### 3. Git Flow

```bash
# Main branches
main                    # Production code
develop                 # Development code

# Supporting branches
feature/feature-name    # New features
release/version         # Release preparation
hotfix/issue            # Critical fixes
```

### 4. .gitignore

```bash
# Tạo file .gitignore
touch .gitignore

# Nội dung mẫu
# Dependencies
node_modules/
vendor/

# Environment files
.env
.env.local

# IDE files
.vscode/
.idea/

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Build files
dist/
build/
```

---

## Tài nguyên học tập

### 1. Tài liệu chính thức
- [Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2)

### 2. Khóa học online
- [Fullstack.edu.vn - Git](https://fullstack.edu.vn/learning/git)
- [GitHub Learning Lab](https://lab.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

### 3. Công cụ hỗ trợ
- **GUI Tools**: GitHub Desktop, GitKraken, SourceTree
- **VS Code Extensions**: GitLens, Git Graph
- **Terminal Tools**: Oh My Zsh Git plugins

### 4. Thực hành
- [Learn Git Branching](https://learngitbranching.js.org/)
- [GitHub](https://github.com/) - Tạo repository và thực hành
- [GitLab](https://gitlab.com/) - Alternative platform

---

## Kết luận

Git là một công cụ mạnh mẽ và cần thiết cho mọi developer. Hãy:

1. **Thực hành thường xuyên** - Tạo project nhỏ để luyện tập
2. **Đọc documentation** - Hiểu sâu các lệnh
3. **Sử dụng GUI tools** - Hỗ trợ visual hóa
4. **Tham gia cộng đồng** - Học từ người khác
5. **Không sợ thử nghiệm** - Git có thể undo hầu hết mọi thứ

> **Lưu ý**: Luôn backup code quan trọng trước khi thử các lệnh Git mới!

---

*Tài liệu này được tạo dựa trên khóa học Git từ [Fullstack.edu.vn](https://fullstack.edu.vn/learning/git?id=d65573db-7d77-4753-83fa-c2f51baabb5d) và kinh nghiệm thực tế trong phát triển phần mềm.*
