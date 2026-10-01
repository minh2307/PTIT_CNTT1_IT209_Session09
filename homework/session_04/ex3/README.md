# Bài 3: Cấu hình xác thực SSH và Đẩy dự án lên GitHub

## 1. Quá trình tạo khóa SSH Ed25519
Để tạo cặp khóa SSH sử dụng thuật toán Ed25519, tôi đã thực hiện câu lệnh sau trong terminal:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- Khi hệ thống hỏi nơi lưu khóa, tôi nhấn Enter để sử dụng đường dẫn mặc định (`~/.ssh/id_ed25519`).
- Tại bước nhập passphrase, tôi có thể thiết lập mật khẩu bảo vệ khóa hoặc nhấn Enter để bỏ qua.

Sau khi tạo xong, bật ssh-agent để quản lý khóa:
```bash
eval "$(ssh-agent -s)"
```

Thêm khóa SSH private vào ssh-agent:
```bash
ssh-add ~/.ssh/id_ed25519
```

Lấy nội dung khóa public (để thêm vào GitHub):
```bash
cat ~/.ssh/id_ed25519.pub
```
Sau đó, truy cập vào trang **Settings** > **SSH and GPG keys** trên GitHub, chọn **New SSH key**, đặt tên cho khóa và dán nội dung khóa public vừa copy vào.

Kiểm tra kết nối SSH tới GitHub bằng lệnh:
```bash
ssh -T git@github.com
```
*Kết quả trả về xác nhận danh tính tài khoản thành công:*
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

## 2. Liên kết remote repository
Trong thư mục dự án cục bộ, tôi khởi tạo git (nếu chưa khởi tạo):
```bash
git init
```

Thêm remote repository bằng đường dẫn URL dạng SSH của GitHub:
```bash
git remote add origin git@github.com:username/repository.git
```

Kiểm tra cấu hình remote URL bằng lệnh:
```bash
git remote -v
```
*Kết quả trả về:*
```
origin  git@github.com:username/repository.git (fetch)
origin  git@github.com:username/repository.git (push)
```

## 3. Đẩy dự án lên GitHub
Thêm toàn bộ file vào staging area và tạo commit:
```bash
git add .
git commit -m "Initial commit for Homework Session 4 Exercise 3"
```

Đổi tên nhánh mặc định thành `main`:
```bash
git branch -M main
```

Đẩy (push) mã nguồn và lịch sử commit lên GitHub:
```bash
git push -u origin main
```

## 4. Đường dẫn URL của kho lưu trữ GitHub
- **URL trang web:** `https://github.com/username/repository`
- **SSH URL:** `git@github.com:username/repository.git`

*(Ghi chú: Giảng viên vui lòng thay thế `username` và `repository` tương ứng với kho lưu trữ thực tế của sinh viên khi kiểm tra hoặc sinh viên cập nhật lại link thực tế của mình vào phần này trước khi nộp)*
