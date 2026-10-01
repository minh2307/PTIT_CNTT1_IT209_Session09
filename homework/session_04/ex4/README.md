# Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Gỡ bỏ file khỏi cache của Git
Trong trường hợp vô tình commit nhầm file chứa thông tin bảo mật (ví dụ: `credentials.txt`), ta cần gỡ bỏ file này khỏi sự theo dõi của Git (cache/index) mà không làm xóa đi file vật lý trên đĩa cứng cục bộ. Lệnh được sử dụng là:

```bash
git rm --cached credentials.txt
```
Lệnh này chỉ gỡ file khỏi Staging Area và bộ nhớ theo dõi của Git, giữ cho file `credentials.txt` vẫn nằm an toàn trên máy tính của bạn.

## 2. Cấu hình tệp tin .gitignore
Sau khi gỡ bỏ khỏi Git cache, để Git tự động bỏ qua file này hoàn toàn trong các commit tương lai, ta tạo một tệp tin ẩn `.gitignore` ở thư mục gốc của dự án và thêm dòng chứa tên file:
```text
credentials.txt
```
Khi chạy lệnh `git status`, Git sẽ hoàn toàn "phớt lờ" và không còn hiển thị `credentials.txt` trong danh sách các tệp đang chờ thêm vào (Untracked files) nữa.

## 3. Chỉnh sửa lịch sử commit gần nhất (Amend)
Để đưa sự thay đổi (bao gồm việc gỡ bỏ file khỏi hệ thống theo dõi và bổ sung tệp `.gitignore`) vào chính commit vừa tạo, đồng thời sửa lại thông điệp commit, ta thêm `.gitignore` vào staging và dùng tùy chọn amend:

```bash
git add .gitignore
git commit --amend -m "Fix: Remove sensitive file (credentials.txt) and ignore it"
```

## 4. Kết quả kiểm tra chứng minh
Chạy lệnh kiểm tra lịch sử commit gần nhất:
```bash
git log -n 1
```

**Kết quả hiển thị mong đợi:**
```
commit abc123def4567890abcdef1234567890abcdef12 (HEAD -> main)
Author: Tên_Học_Vên <email_cua_ban@example.com>
Date:   Thu Oct 1 22:45:00 2026 +0700

    Fix: Remove sensitive file (credentials.txt) and ignore it
```
*Như kết quả trên, `credentials.txt` đã được gỡ bỏ khỏi lịch sử và thông điệp commit đã được cập nhật thành công.*
