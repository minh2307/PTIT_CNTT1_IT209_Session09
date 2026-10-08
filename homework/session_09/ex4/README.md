# Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume

## Các lệnh đã thực hiện

1. Tạo một Named Volume:
```bash
docker volume create easy-volume
```

2. Dùng container Alpine ghi nội dung vào volume:
```bash
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
```

3. Dùng container Alpine thứ hai đọc lại tệp đó để kiểm tra:
```bash
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
```

**Kết quả sau khi chạy lệnh đọc tệp:**
```text
Luu tru du lieu Docker
```
