# Bài 3: Viết Dockerfile đóng gói trang Web HTML tĩnh

## Các lệnh kiểm tra

1. Build image:
```bash
docker build -t my-html-app:v1 .
```

2. Khởi chạy container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

3. Kiểm tra kết quả:
```bash
curl http://localhost:8081
```

Kết quả mong đợi: `<h1>Hello Docker Session 09!</h1>`
