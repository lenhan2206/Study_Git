# 📚 Hướng Dẫn Học Git - Từ Cơ Bản Đến Nâng Cao

## 📋 Mục Lục
1. [🎯 Giới thiệu về Git](#-giới-thiệu-về-git)
2. [⚙️ Cài đặt và Cấu hình](#️-cài-đặt-và-cấu-hình)
3. [🚀 Khởi tạo Repository](#-khởi-tạo-repository)
4. [📝 Các thao tác cơ bản](#-các-thao-tác-cơ-bản)
5. [🌿 Làm việc với Branch](#-làm-việc-với-branch)
6. [☁️ Remote Repository](#️-remote-repository)
7. [⚔️ Giải quyết xung đột](#️-giải-quyết-xung-đột)
8. [🔧 Các lệnh nâng cao](#-các-lệnh-nâng-cao)
9. [✨ Best Practices](#-best-practices)
10. [📖 Tài nguyên học tập](#-tài-nguyên-học-tập)

---

## 🎯 Giới thiệu về Git

### Git là gì?
Git là một **hệ thống quản lý phiên bản phân tán** (Distributed Version Control System) được phát triển bởi Linus Torvalds vào năm 2005. Git giúp:

- **📊 Theo dõi thay đổi**: Ghi lại mọi thay đổi trong code với timestamp và tác giả
- **👥 Làm việc nhóm**: Nhiều người có thể cùng làm việc trên một dự án mà không ảnh hưởng lẫn nhau
- **⏪ Khôi phục**: Quay lại bất kỳ phiên bản nào trước đó một cách dễ dàng
- **🌿 Phân nhánh**: Tạo các nhánh để phát triển tính năng mới mà không ảnh hưởng code chính

### 🔍 Tại sao cần Git?

#### Trước khi có Git:
```
📁 Project/
├── 📄 index.html
├── 📄 index.html.backup
├── 📄 index.html.old
├── 📄 index.html.final
└── 📄 index.html.final.final
```
**❌ Vấn đề**: Không biết file nào là phiên bản mới nhất, ai đã thay đổi gì, khi nào thay đổi.

#### Sau khi có Git:
```
📁 Project/
├── 📄 index.html
└── 📁 .git/ (chứa toàn bộ lịch sử)
```
**✅ Giải pháp**: Git quản lý tất cả lịch sử, có thể xem ai thay đổi gì, khi nào, và tại sao.

### 🏗️ Kiến trúc Git

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Working Dir   │    │   Staging Area  │    │   Repository    │
│                 │    │                 │    │                 │
│ 📄 file1.txt    │───▶│ 📄 file1.txt    │───▶│ 📄 file1.txt    │
│ 📄 file2.txt    │    │                 │    │ 📄 file2.txt    │
│ 📄 file3.txt    │    │                 │    │ 📄 file3.txt    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
        │                        │                        │
        │ git add                │ git commit             │
        ▼                        ▼                        ▼
   Modified files          Staged files              Committed files
```

---

## ⚙️ Cài đặt và Cấu hình

### 1. 📥 Cài đặt Git

#### 🪟 Windows
```bash
# Cách 1: Tải từ trang chủ
# Truy cập: https://git-scm.com/download/win
# Tải và cài đặt Git for Windows

# Cách 2: Sử dụng Chocolatey
choco install git

# Cách 3: Sử dụng winget (Windows 10/11)
winget install Git.Git

# Cách 4: Sử dụng Scoop
scoop install git
```

#### 🍎 macOS
```bash
# Cách 1: Sử dụng Homebrew (khuyến nghị)
brew install git

# Cách 2: Sử dụng MacPorts
sudo port install git

# Cách 3: Tải từ trang chủ
# Truy cập: https://git-scm.com/download/mac
```

#### 🐧 Linux (Ubuntu/Debian)
```bash
# Cập nhật package list
sudo apt update

# Cài đặt Git
sudo apt install git

# Kiểm tra phiên bản
git --version
```

#### 🐧 Linux (CentOS/RHEL/Fedora)
```bash
# CentOS/RHEL
sudo yum install git

# Fedora
sudo dnf install git
```

### 2. ⚙️ Cấu hình Git

#### 🔧 Cấu hình cơ bản
```bash
# Cấu hình tên người dùng (bắt buộc)
git config --global user.name "Nguyen Van A"

# Cấu hình email (bắt buộc)
git config --global user.email "nguyenvana@example.com"

# Kiểm tra cấu hình hiện tại
git config --list

# Xem cấu hình cụ thể
git config user.name
git config user.email
```

#### 🎨 Cấu hình nâng cao
```bash
# Đặt editor mặc định
git config --global core.editor "code --wait"        # VS Code
git config --global core.editor "notepad++"          # Notepad++
git config --global core.editor "vim"                # Vim

# Đặt branch mặc định (Git 2.28+)
git config --global init.defaultBranch main

# Cấu hình line ending
git config --global core.autocrlf true               # Windows
git config --global core.autocrlf input              # macOS/Linux

# Cấu hình màu sắc
git config --global color.ui auto

# Cấu hình alias (tên viết tắt)
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
```

#### 📝 Ví dụ cấu hình hoàn chỉnh
```bash
# Thiết lập cho developer mới
git config --global user.name "Le Nhan"
git config --global user.email "lenhan2206@gmail.com"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main
git config --global core.autocrlf true
git config --global color.ui auto

# Tạo alias hữu ích
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

---

## 🚀 Khởi tạo Repository

### 1. 🆕 Tạo Repository mới

#### 📁 Tạo thư mục và khởi tạo Git
```bash
# Tạo thư mục dự án
mkdir my-awesome-project
cd my-awesome-project

# Khởi tạo Git repository
git init

# Kết quả:
# Initialized empty Git repository in /path/to/my-awesome-project/.git/
```

#### 🔍 Kiểm tra trạng thái
```bash
# Kiểm tra trạng thái repository
git status

# Kết quả:
# On branch main
# 
# No commits yet
# 
# nothing to commit (create/copy files and track them)
```

#### 📄 Tạo file đầu tiên
```bash
# Tạo file README
echo "# My Awesome Project" > README.md

# Tạo file index.html
cat > index.html << EOF
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Awesome Project</title>
</head>
<body>
    <h1>Welcome to My Project!</h1>
    <p>This is my first Git repository.</p>
</body>
</html>
EOF

# Kiểm tra trạng thái
git status
```

### 2. 📥 Clone Repository có sẵn

#### 🔗 Clone từ GitHub/GitLab
```bash
# Clone repository public
git clone https://github.com/username/repository.git

# Clone với tên thư mục tùy chỉnh
git clone https://github.com/username/repository.git my-custom-name

# Clone chỉ nhánh cụ thể
git clone -b feature-branch https://github.com/username/repository.git

# Clone với SSH (cần setup SSH key)
git clone git@github.com:username/repository.git
```

#### 📋 Ví dụ thực tế
```bash
# Clone repository React mẫu
git clone https://github.com/facebook/create-react-app.git

# Clone vào thư mục tùy chỉnh
git clone https://github.com/facebook/create-react-app.git react-tutorial

# Clone chỉ nhánh main
git clone -b main https://github.com/facebook/create-react-app.git
```

#### 🔐 Clone repository private
```bash
# Sử dụng Personal Access Token
git clone https://username:token@github.com/username/private-repo.git

# Sử dụng SSH (khuyến nghị)
git clone git@github.com:username/private-repo.git
```

---

## 📝 Các thao tác cơ bản

### 1. 🔄 Workflow cơ bản

#### 📊 Sơ đồ workflow
```
Working Directory → Staging Area → Repository
      │                │              │
      │ git add        │ git commit   │
      ▼                ▼              ▼
   Modified files → Staged files → Committed files
```

#### 🛠️ Các bước thực hiện
```bash
# Bước 1: Kiểm tra trạng thái
git status

# Bước 2: Thêm file vào staging area
git add filename.txt
git add .                    # Thêm tất cả file
git add *.js                 # Thêm tất cả file .js

# Bước 3: Commit thay đổi
git commit -m "Thông điệp commit"

# Bước 4: Xem lịch sử
git log
```

### 2. 📊 Kiểm tra trạng thái

#### 🔍 Lệnh git status
```bash
# Trạng thái tổng quan
git status

# Ví dụ output:
# On branch main
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
# 
#         modified:   index.html
# 
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
# 
#         new-file.txt
# 
# no changes added to commit (use "git add" or "git commit -a")

# Trạng thái ngắn gọn
git status --short
# M  index.html
# ?? new-file.txt

# Trạng thái với branch info
git status -b
```

#### 🔍 Lệnh git diff
```bash
# Xem thay đổi chưa staged
git diff

# Ví dụ output:
# diff --git a/index.html b/index.html
# index 1234567..abcdefg 100644
# --- a/index.html
# +++ b/index.html
# @@ -1,7 +1,7 @@
#  <!DOCTYPE html>
#  <html lang="en">
#  <head>
#      <meta charset="UTF-8">
# -    <title>Old Title</title>
# +    <title>New Title</title>
#  </head>

# Xem thay đổi đã staged
git diff --staged
git diff --cached

# Xem thay đổi giữa 2 commit
git diff HEAD~1 HEAD
git diff commit1 commit2
```

### 3. ➕ Thêm file

#### 📁 Các cách thêm file
```bash
# Thêm file cụ thể
git add index.html
git add src/components/Header.js

# Thêm tất cả file
git add .

# Thêm tất cả file (bao gồm file đã xóa)
git add -A
git add --all

# Chỉ thêm file đã được track
git add -u
git add --update

# Thêm file theo pattern
git add *.js              # Tất cả file .js
git add src/*.css         # Tất cả file .css trong thư mục src
git add "*.txt"           # Tất cả file .txt
```

#### 📝 Ví dụ thực tế
```bash
# Tạo project React
mkdir react-app
cd react-app
git init

# Tạo các file
echo "console.log('Hello World');" > index.js
echo "body { margin: 0; }" > style.css
echo "# React App" > README.md

# Thêm từng file
git add index.js
git add style.css
git add README.md

# Hoặc thêm tất cả
git add .

# Kiểm tra trạng thái
git status
```

### 4. 💾 Commit

#### 📝 Các cách commit
```bash
# Commit với message
git commit -m "Add new feature"

# Commit với message dài
git commit -m "Add user authentication
- Implement login functionality
- Add password validation
- Create user session management"

# Add và commit cùng lúc (chỉ với file đã track)
git commit -am "Update existing files"

# Commit với editor
git commit

# Sửa commit cuối cùng
git commit --amend -m "New commit message"
```

#### 📋 Ví dụ commit message tốt
```bash
# ✅ Tốt - Rõ ràng, ngắn gọn
git commit -m "feat: add user login functionality"
git commit -m "fix: resolve button alignment issue"
git commit -m "docs: update installation guide"
git commit -m "refactor: simplify user service logic"
git commit -m "test: add unit tests for login component"

# ❌ Tốt - Không rõ ràng
git commit -m "update"
git commit -m "fix bug"
git commit -m "changes"
git commit -m "work in progress"
```

### 5. 📜 Xem lịch sử

#### 📊 Các lệnh git log
```bash
# Lịch sử đầy đủ
git log

# Lịch sử ngắn gọn
git log --oneline

# Lịch sử với biểu đồ
git log --graph --oneline

# Lịch sử với thống kê
git log --stat

# Lịch sử với patch
git log -p

# Lịch sử theo tác giả
git log --author="Nguyen Van A"

# Lịch sử theo thời gian
git log --since="2024-01-01"
git log --until="2024-12-31"
git log --since="2 weeks ago"

# Lịch sử theo file
git log -- index.html
git log --follow index.html  # Theo dõi file đã rename
```

#### 📋 Ví dụ output git log
```bash
$ git log --oneline --graph
* a1b2c3d (HEAD -> main) feat: add user authentication
* e4f5g6h fix: resolve login button issue
* i7j8k9l docs: update README
* m1n2o3p Initial commit
```

### 6. ⏪ Undo và Reset

#### 🔄 Undo thay đổi chưa staged
```bash
# Undo thay đổi file cụ thể
git checkout -- filename.txt
git restore filename.txt

# Undo tất cả thay đổi
git checkout -- .
git restore .

# Ví dụ thực tế
echo "New content" >> index.html
git status  # Shows modified
git restore index.html
git status  # Clean working directory
```

#### 🔄 Undo thay đổi đã staged
```bash
# Undo file cụ thể
git reset HEAD filename.txt
git restore --staged filename.txt

# Undo tất cả staged files
git reset HEAD
git restore --staged .

# Ví dụ thực tế
git add index.html
git status  # Shows staged
git restore --staged index.html
git status  # Shows modified but not staged
```

#### 🔄 Undo commit
```bash
# Undo commit cuối cùng (giữ thay đổi)
git reset --soft HEAD~1

# Undo commit cuối cùng (xóa thay đổi)
git reset --hard HEAD~1

# Undo nhiều commit
git reset --soft HEAD~3

# Ví dụ thực tế
git log --oneline
# a1b2c3d (HEAD -> main) feat: add user auth
# e4f5g6h fix: login button
# i7j8k9l docs: update README

git reset --soft HEAD~1
git status  # Shows staged changes from the undone commit
```

---

## 🌿 Làm việc với Branch

### 1. 🌱 Tạo và chuyển đổi Branch

#### 📊 Sơ đồ branch
```
main ──────●──────●──────●
            \              \
feature ─────●──────●──────●
```

#### 🛠️ Các lệnh branch
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

#### 📝 Ví dụ thực tế
```bash
# Tạo project và commit đầu tiên
mkdir branch-demo
cd branch-demo
git init
echo "# Branch Demo" > README.md
git add README.md
git commit -m "Initial commit"

# Tạo branch mới cho feature
git checkout -b feature/user-auth

# Làm việc trên feature branch
echo "// User authentication logic" > auth.js
git add auth.js
git commit -m "Add user authentication"

# Chuyển về main
git checkout main

# Tạo branch khác
git checkout -b feature/payment

# Làm việc trên payment branch
echo "// Payment processing logic" > payment.js
git add payment.js
git commit -m "Add payment processing"

# Xem tất cả branches
git branch -a
```

### 2. 🔀 Merge Branch

#### 📊 Sơ đồ merge
```
Before merge:
main ──────●──────●
            \      \
feature ─────●──────●

After merge:
main ──────●──────●──────● (merge commit)
            \      \      /
feature ─────●──────●────
```

#### 🛠️ Các lệnh merge
```bash
# Chuyển về branch chính
git checkout main

# Merge branch
git merge feature-branch

# Merge với no-fast-forward
git merge --no-ff feature-branch

# Merge với squash
git merge --squash feature-branch

# Xóa branch đã merge
git branch -d feature-branch
```

#### 📝 Ví dụ merge thực tế
```bash
# Tạo conflict để demo
git checkout main
echo "console.log('Main version');" > app.js
git add app.js
git commit -m "Add app.js to main"

git checkout -b feature/new-feature
echo "console.log('Feature version');" > app.js
git add app.js
git commit -m "Update app.js in feature"

# Merge feature vào main
git checkout main
git merge feature/new-feature

# Kết quả: Fast-forward merge
git log --oneline --graph
```

### 3. 🔄 Rebase

#### 📊 Sơ đồ rebase
```
Before rebase:
main ──────●──────●──────●
            \      \
feature ─────●──────●

After rebase:
main ──────●──────●──────●
                      \    \
feature ───────────────●────●
```

#### 🛠️ Các lệnh rebase
```bash
# Rebase branch hiện tại lên main
git rebase main

# Interactive rebase
git rebase -i HEAD~3

# Rebase với conflict resolution
git rebase main
# Resolve conflicts
git add .
git rebase --continue

# Abort rebase
git rebase --abort
```

#### 📝 Ví dụ rebase thực tế
```bash
# Tạo commits trên feature branch
git checkout -b feature/rebase-demo
echo "// Feature 1" > feature1.js
git add feature1.js
git commit -m "Add feature 1"

echo "// Feature 2" > feature2.js
git add feature2.js
git commit -m "Add feature 2"

# Tạo commit trên main
git checkout main
echo "// Main update" > main.js
git add main.js
git commit -m "Update main"

# Rebase feature lên main
git checkout feature/rebase-demo
git rebase main

# Kết quả: Linear history
git log --oneline --graph
```

---

## ☁️ Remote Repository

### 1. 🔗 Thêm Remote

#### 🛠️ Các lệnh remote
```bash
# Thêm remote origin
git remote add origin https://github.com/username/repo.git

# Xem danh sách remote
git remote -v

# Xem thông tin remote
git remote show origin

# Thay đổi URL remote
git remote set-url origin new-url

# Xóa remote
git remote remove origin
```

#### 📝 Ví dụ thực tế
```bash
# Tạo repository local
mkdir my-project
cd my-project
git init
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"

# Thêm remote GitHub
git remote add origin https://github.com/lenhan2206/Study_Git.git

# Kiểm tra remote
git remote -v
# origin  https://github.com/lenhan2206/Study_Git.git (fetch)
# origin  https://github.com/lenhan2206/Study_Git.git (push)
```

### 2. 📤 Push và Pull

#### 📊 Sơ đồ push/pull
```
Local Repository ←→ Remote Repository
       │                    │
       │ git push           │
       ▼                    │
   Upload changes ──────────┘
       │                    │
       │ git pull           │
       ▲                    │
   Download changes ←────────┘
```

#### 🛠️ Các lệnh push/pull
```bash
# Push lần đầu
git push -u origin main

# Push thông thường
git push origin main
git push origin feature-branch

# Push tất cả branches
git push --all origin

# Push tags
git push origin --tags

# Pull thay đổi
git pull origin main

# Fetch thay đổi (không merge)
git fetch origin
git merge origin/main
```

#### 📝 Ví dụ push/pull thực tế
```bash
# Push lần đầu
git push -u origin main
# Branch 'main' set up to track remote branch 'main' from 'origin'.

# Tạo thay đổi mới
echo "// New feature" > new-feature.js
git add new-feature.js
git commit -m "Add new feature"

# Push thay đổi
git push origin main

# Simulate changes from another developer
# (On GitHub, edit README.md)

# Pull thay đổi
git pull origin main
```

### 3. 🍴 Fork và Pull Request

#### 📊 Sơ đồ fork workflow
```
Original Repo ──────●──────●──────●
                     │
                     │ Fork
                     ▼
Your Fork ──────────●──────●──────●
                     │
                     │ Pull Request
                     ▼
Original Repo ──────●──────●──────●──────● (merged)
```

#### 🛠️ Các bước fork workflow
```bash
# 1. Fork repository trên GitHub
# 2. Clone fork về máy
git clone https://github.com/your-username/forked-repo.git

# 3. Thêm upstream
git remote add upstream https://github.com/original-owner/repo.git

# 4. Sync với upstream
git fetch upstream
git checkout main
git merge upstream/main

# 5. Tạo feature branch
git checkout -b feature/your-feature

# 6. Làm việc và commit
echo "// Your changes" > your-file.js
git add your-file.js
git commit -m "Add your feature"

# 7. Push feature branch
git push origin feature/your-feature

# 8. Tạo Pull Request trên GitHub
```

#### 📝 Ví dụ fork workflow thực tế
```bash
# Clone fork
git clone https://github.com/lenhan2206/Study_Git.git
cd Study_Git

# Thêm upstream
git remote add upstream https://github.com/original-owner/Study_Git.git

# Kiểm tra remotes
git remote -v
# origin    https://github.com/lenhan2206/Study_Git.git (fetch)
# origin    https://github.com/lenhan2206/Study_Git.git (push)
# upstream  https://github.com/original-owner/Study_Git.git (fetch)
# upstream  https://github.com/original-owner/Study_Git.git (push)

# Sync với upstream
git fetch upstream
git checkout main
git merge upstream/main

# Tạo feature branch
git checkout -b feature/improve-docs
echo "## New Section" >> Git_Tutorial.md
git add Git_Tutorial.md
git commit -m "docs: add new section to tutorial"
git push origin feature/improve-docs
```

---

## ⚔️ Giải quyết xung đột

### 1. 🔍 Khi nào xảy ra xung đột?

#### 📊 Các trường hợp xung đột
```bash
# 1. Merge conflict
git checkout main
echo "console.log('Main version');" > app.js
git add app.js
git commit -m "Add app.js to main"

git checkout -b feature
echo "console.log('Feature version');" > app.js
git add app.js
git commit -m "Update app.js in feature"

git checkout main
git merge feature
# Auto-merging app.js
# CONFLICT (content): Merge conflict in app.js
# Automatic merge failed; fix conflicts and then commit the result.
```

#### 📋 Ví dụ conflict markers
```javascript
// app.js
<<<<<<< HEAD
console.log('Main version');
=======
console.log('Feature version');
>>>>>>> feature
```

### 2. 🛠️ Cách giải quyết xung đột

#### 📝 Các bước giải quyết
```bash
# 1. Git báo xung đột
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

#### 📝 Ví dụ giải quyết conflict
```bash
# Tạo conflict
git checkout main
echo "console.log('Hello from main');" > greeting.js
git add greeting.js
git commit -m "Add greeting to main"

git checkout -b feature/greeting
echo "console.log('Hello from feature');" > greeting.js
git add greeting.js
git commit -m "Update greeting in feature"

# Merge và tạo conflict
git checkout main
git merge feature/greeting

# File greeting.js có conflict:
# <<<<<<< HEAD
# console.log('Hello from main');
# =======
# console.log('Hello from feature');
# >>>>>>> feature/greeting

# Giải quyết conflict
echo "console.log('Hello from both!');" > greeting.js
git add greeting.js
git commit -m "Resolve greeting conflict"
```

### 3. 🔧 Công cụ hỗ trợ

#### 🛠️ Merge tools
```bash
# Sử dụng merge tool
git mergetool

# Cấu hình merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Các merge tool phổ biến
git config --global merge.tool vimdiff
git config --global merge.tool kdiff3
git config --global merge.tool meld
```

#### 📝 Ví dụ sử dụng merge tool
```bash
# Cấu hình VS Code làm merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Khi có conflict
git merge feature-branch
git mergetool
# VS Code sẽ mở với 3 panels: local, base, remote
```

---

## 🔧 Các lệnh nâng cao

### 1. 💾 Stash

#### 📊 Sơ đồ stash
```
Working Directory → Stash → Working Directory
      │              │              │
      │ git stash    │ git stash    │
      ▼              │ pop/apply    ▼
   Clean state ←─────┘              Restored changes
```

#### 🛠️ Các lệnh stash
```bash
# Lưu thay đổi tạm thời
git stash
git stash save "Message"

# Xem danh sách stash
git stash list

# Áp dụng stash
git stash apply
git stash pop

# Áp dụng stash cụ thể
git stash apply stash@{0}

# Xóa stash
git stash drop
git stash clear
```

#### 📝 Ví dụ stash thực tế
```bash
# Đang làm việc trên feature
echo "// Working on feature" > feature.js
git add feature.js

# Cần chuyển sang branch khác
git stash save "WIP: working on feature"

# Chuyển sang branch khác
git checkout main
echo "// Fix urgent bug" > bugfix.js
git add bugfix.js
git commit -m "Fix urgent bug"

# Quay lại feature branch
git checkout feature
git stash pop
# Working on feature
```

### 2. 🍒 Cherry-pick

#### 📊 Sơ đồ cherry-pick
```
Branch A: ●────●────●────●
              │
              │ cherry-pick
              ▼
Branch B: ●────●────●────●────●
```

#### 🛠️ Các lệnh cherry-pick
```bash
# Lấy commit từ branch khác
git cherry-pick commit-hash

# Cherry-pick nhiều commit
git cherry-pick commit1 commit2

# Cherry-pick range
git cherry-pick commit1..commit3

# Cherry-pick với no-commit
git cherry-pick --no-commit commit-hash
```

#### 📝 Ví dụ cherry-pick thực tế
```bash
# Tạo commits trên feature branch
git checkout -b feature/auth
echo "// Auth logic" > auth.js
git add auth.js
git commit -m "Add authentication"

echo "// Auth tests" > auth.test.js
git add auth.test.js
git commit -m "Add auth tests"

# Cherry-pick commit đầu tiên vào main
git checkout main
git cherry-pick <commit-hash-of-auth-logic>

# Kết quả: Chỉ có auth.js được thêm vào main
```

### 3. 🏷️ Tag

#### 📊 Sơ đồ tag
```
main: ●────●────●────●────●
       v1.0  v1.1  v1.2  v2.0
```

#### 🛠️ Các lệnh tag
```bash
# Tạo lightweight tag
git tag v1.0.0

# Tạo annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Xem danh sách tag
git tag
git tag -l "v1.*"

# Xem thông tin tag
git show v1.0.0

# Push tag
git push origin v1.0.0
git push origin --tags

# Xóa tag
git tag -d v1.0.0
git push origin --delete v1.0.0
```

#### 📝 Ví dụ tag thực tế
```bash
# Tạo release
echo "// Version 1.0.0" > version.js
git add version.js
git commit -m "Release version 1.0.0"

# Tạo tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tag
git push origin v1.0.0

# Tạo hotfix
echo "// Bug fix" > fix.js
git add fix.js
git commit -m "Fix critical bug"
git tag -a v1.0.1 -m "Hotfix version 1.0.1"
git push origin v1.0.1
```

### 4. 📦 Submodule

#### 📊 Sơ đồ submodule
```
Main Project/
├── src/
├── docs/
└── external-lib/ (submodule)
    └── external-project/
```

#### 🛠️ Các lệnh submodule
```bash
# Thêm submodule
git submodule add https://github.com/user/repo.git path/to/submodule

# Clone repository có submodule
git clone --recursive https://github.com/user/repo.git

# Update submodule
git submodule update --remote

# Xóa submodule
git submodule deinit path/to/submodule
git rm path/to/submodule
```

#### 📝 Ví dụ submodule thực tế
```bash
# Thêm Bootstrap làm submodule
git submodule add https://github.com/twbs/bootstrap.git vendor/bootstrap

# Commit submodule
git add .gitmodules vendor/bootstrap
git commit -m "Add Bootstrap as submodule"

# Clone project với submodule
git clone --recursive https://github.com/user/project.git

# Update Bootstrap
git submodule update --remote vendor/bootstrap
```

---

## ✨ Best Practices

### 1. 📝 Commit Message

#### 📋 Format chuẩn (Conventional Commits)
```bash
type(scope): description

# Types:
feat:     # New feature
fix:      # Bug fix
docs:     # Documentation
style:    # Code style changes
refactor: # Code refactoring
test:     # Adding tests
chore:    # Maintenance tasks
```

#### 📝 Ví dụ commit message tốt
```bash
# ✅ Tốt
feat(auth): add user login functionality
fix(ui): resolve button alignment issue
docs(readme): update installation guide
refactor(api): simplify user service
test(auth): add unit tests for login
chore(deps): update dependencies

# ❌ Không tốt
update
fix bug
changes
work in progress
asdf
```

#### 📋 Template commit message
```bash
# Tạo template
git config --global commit.template ~/.gitmessage

# Nội dung template:
# type(scope): brief description
#
# Detailed description of changes
#
# - Bullet point 1
# - Bullet point 2
#
# Closes #123
```

### 2. 🌿 Branch Naming

#### 📋 Quy tắc đặt tên branch
```bash
# Feature branches
feature/user-authentication
feature/payment-integration
feature/dashboard-redesign

# Bug fix branches
bugfix/login-error
bugfix/memory-leak
hotfix/security-patch

# Release branches
release/v1.2.0
release/v2.0.0

# Experimental branches
experiment/new-algorithm
spike/performance-test
```

#### 📝 Ví dụ branch workflow
```bash
# Tạo feature branch
git checkout -b feature/user-profile

# Làm việc và commit
echo "// User profile component" > UserProfile.js
git add UserProfile.js
git commit -m "feat(profile): add user profile component"

# Push branch
git push origin feature/user-profile

# Tạo Pull Request
# Merge sau khi review
```

### 3. 🔄 Git Flow

#### 📊 Sơ đồ Git Flow
```
main ──────●──────●──────●──────●
            \      \      \      \
develop ─────●──────●──────●──────●
              \      \      \
feature ───────●──────●──────●
                \      \
release ─────────●──────●
                  \
hotfix ────────────●
```

#### 🛠️ Các branch chính
```bash
# Main branches
main                    # Production code
develop                 # Development code

# Supporting branches
feature/feature-name    # New features
release/version         # Release preparation
hotfix/issue            # Critical fixes
```

#### 📝 Ví dụ Git Flow
```bash
# Khởi tạo Git Flow
git flow init

# Tạo feature
git flow feature start user-auth
# Tương đương: git checkout -b feature/user-auth

# Hoàn thành feature
git flow feature finish user-auth
# Tương đương: git checkout develop && git merge feature/user-auth

# Tạo release
git flow release start 1.0.0
# Tương đương: git checkout -b release/1.0.0
```

### 4. 📄 .gitignore

#### 📋 Tạo file .gitignore
```bash
# Tạo file .gitignore
touch .gitignore
```

#### 📝 Nội dung .gitignore mẫu
```bash
# Dependencies
node_modules/
vendor/
bower_components/

# Environment files
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# IDE files
.vscode/
.idea/
*.swp
*.swo
*~

# OS files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# Logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
logs/

# Build files
dist/
build/
out/
target/

# Cache
.cache/
.parcel-cache/
.next/
.nuxt/

# Coverage
coverage/
.nyc_output/

# Temporary files
*.tmp
*.temp
```

#### 📝 Ví dụ .gitignore cho các project
```bash
# React project
node_modules/
build/
.env
.DS_Store

# Node.js project
node_modules/
npm-debug.log*
.env
dist/

# Python project
__pycache__/
*.py[cod]
*$py.class
.env
venv/
env/

# Java project
target/
*.class
*.jar
*.war
.idea/
```

---

## 📖 Tài nguyên học tập

### 1. 📚 Tài liệu chính thức
- [Git Documentation](https://git-scm.com/doc) - Tài liệu chính thức
- [Pro Git Book](https://git-scm.com/book/en/v2) - Cuốn sách miễn phí về Git
- [Git Reference](https://git-scm.com/docs) - Tham khảo đầy đủ các lệnh

### 2. 🎓 Khóa học online
- [Fullstack.edu.vn - Git](https://fullstack.edu.vn/learning/git) - Khóa học tiếng Việt
- [GitHub Learning Lab](https://lab.github.com/) - Học Git qua thực hành
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials) - Hướng dẫn chi tiết
- [Learn Git Branching](https://learngitbranching.js.org/) - Học Git qua game

### 3. 🛠️ Công cụ hỗ trợ

#### 🖥️ GUI Tools
- **GitHub Desktop** - Giao diện đơn giản cho GitHub
- **GitKraken** - Giao diện đẹp với nhiều tính năng
- **SourceTree** - Công cụ mạnh mẽ từ Atlassian
- **TortoiseGit** - Tích hợp với Windows Explorer

#### 🔌 VS Code Extensions
- **GitLens** - Tăng cường khả năng Git trong VS Code
- **Git Graph** - Xem biểu đồ Git
- **Git History** - Xem lịch sử file
- **Git Blame** - Xem ai đã sửa dòng nào

#### 🖥️ Terminal Tools
- **Oh My Zsh Git plugins** - Tăng cường terminal
- **Git Bash** - Terminal Git cho Windows
- **PowerShell Git** - Git trong PowerShell

### 4. 🎯 Thực hành

#### 🌐 Platforms
- [GitHub](https://github.com/) - Tạo repository và thực hành
- [GitLab](https://gitlab.com/) - Alternative platform
- [Bitbucket](https://bitbucket.org/) - Platform của Atlassian

#### 🎮 Interactive Learning
- [Learn Git Branching](https://learngitbranching.js.org/) - Game học Git
- [Git-it](https://github.com/jlord/git-it-electron) - Desktop app học Git
- [Try Git](https://try.github.io/) - Hướng dẫn tương tác

### 5. 📱 Mobile Apps
- **GitHub Mobile** - Quản lý repository trên mobile
- **GitLab Mobile** - GitLab trên mobile
- **Working Copy** - Git client cho iOS

---

## 🎯 Kết luận

### 🚀 Tóm tắt kiến thức quan trọng

1. **Git là gì**: Hệ thống quản lý phiên bản phân tán
2. **Workflow cơ bản**: Working Directory → Staging → Repository
3. **Branch**: Tạo nhánh để phát triển tính năng mới
4. **Merge/Rebase**: Hợp nhất thay đổi từ các nhánh
5. **Remote**: Làm việc với repository trên server
6. **Conflict**: Giải quyết xung đột khi merge

### 💡 Lời khuyên cho người mới

1. **Thực hành thường xuyên** - Tạo project nhỏ để luyện tập
2. **Đọc documentation** - Hiểu sâu các lệnh và options
3. **Sử dụng GUI tools** - Hỗ trợ visual hóa workflow
4. **Tham gia cộng đồng** - Học từ người khác qua Pull Request
5. **Không sợ thử nghiệm** - Git có thể undo hầu hết mọi thứ

### ⚠️ Lưu ý quan trọng

- **Luôn backup code quan trọng** trước khi thử các lệnh Git mới
- **Commit thường xuyên** với message rõ ràng
- **Sử dụng .gitignore** để tránh commit file không cần thiết
- **Review code** trước khi merge vào main branch
- **Giữ history sạch sẽ** với commit message có ý nghĩa

### 🎉 Chúc mừng!

Bạn đã hoàn thành hướng dẫn Git từ cơ bản đến nâng cao. Hãy tiếp tục thực hành và khám phá thêm các tính năng mạnh mẽ của Git!

---

*📝 Tài liệu này được tạo dựa trên khóa học Git từ [Fullstack.edu.vn](https://fullstack.edu.vn/learning/git?id=d65573db-7d77-4753-83fa-c2f51baabb5d) và kinh nghiệm thực tế trong phát triển phần mềm.*

*🔄 Cập nhật lần cuối: $(date)*

*👨‍💻 Tác giả: Le Nhan - [GitHub](https://github.com/lenhan2206)*
