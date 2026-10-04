# Bài 1: Thay đổi cổng kết nối SSH (SSH Port Hardening)

### 1. Thay đổi cấu hình cổng SSH
Sử dụng quyền `sudo` để mở file cấu hình của SSH Daemon:
```bash
sudo nano /etc/ssh/sshd_config
```
Tìm đến dòng `#Port 22` hoặc `Port 22`. Xóa dấu `#` (nếu có) và sửa thành:
```
Port 2222
```
Lưu lại file và thoát.

### 2. Cấu hình tường lửa UFW
Mở cổng 2222 trên tường lửa UFW trước khi khởi động lại dịch vụ SSH (để tránh bị mất quyền truy cập):
```bash
sudo ufw allow 2222/tcp
```

### 3. Khởi động lại dịch vụ SSH
Áp dụng cấu hình mới:
```bash
sudo systemctl restart ssh
# Hoặc trên một số hệ thống: sudo systemctl restart sshd
```

### 4. Kiểm tra kết nối
*Lưu ý: Vì thẻ visa của em bị khoá nên không thể tạo droplet để chụp lại bằng chứng chạy thật lệnh này. Các lệnh dưới đây là lệnh lý thuyết.*

Mở một Terminal mới (không đóng terminal hiện tại để dự phòng) và thử kết nối qua cổng mới:
```bash
ssh -p 2222 devops@<IP_ADDRESS_DROPLET>
```
*(Kết nối sẽ thành công).*

Kiểm tra kết nối qua cổng mặc định cũ (22):
```bash
ssh -p 22 devops@<IP_ADDRESS_DROPLET>
```
*(Kết nối sẽ bị chặn và báo lỗi Connection refused hoặc Timeout).*
