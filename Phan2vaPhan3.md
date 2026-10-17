# :rocket: SMART-FARM: Hệ thống IoT cho trang trại Lan

![Sơ đồ kiến trúc](https://rikkeiedu-storage.s3.ap-southeast-2.amazonaws.com/uploads/editor-images/1787648283613_687ec2e7-229c-4942-a347-080fae59560a.webp)

---

## 1. Quy trình xử lý thông tin DIKW
1. **Data:** Nhận chuỗi thô từ cảm biến (Ví dụ: `38.5`).
2. **Information:** Phân tích cú pháp: *"Nhiệt độ Zone 1 là 38.5°C"*.
3. **Knowledge:** Đối chiếu tri thức: *Lan sẽ cháy lá nếu nhiệt độ vượt ngưỡng `35°C`*.
4. **Wisdom:** Hành động: Tự động kích hoạt máy bơm phun sương làm mát.

---

## 2. Chu kỳ Fetch-Decode-Execute của CPU
> **Fetch:** CPU truy xuất mã lệnh tưới nước từ RAM.
> **Decode:** Khối giải mã phân tích lệnh, xác định cần xuất tín hiệu mức High ra chân GPIO rơ-le.
> **Execute:** Đơn vị ALU phát tín hiệu điện đóng mạch rơ-le, kích hoạt máy bơm phun sương.

---

## 3. Tính năng & Tiến độ
- [x] Đọc dữ liệu môi trường thời gian thực từ DHT22.
- [x] Tự động bật quạt hút làm mát khi quá nhiệt.
- [x] Ghi nhật ký vận hành vào tệp `system.log`.
- [ ] Tích hợp gửi cảnh báo khẩn cấp qua Telegram.

---

## 4. Bảng thông số kỹ thuật

| Linh kiện | Vai trò IPO | Thông số hoạt động | Trạng thái |
| :--- | :--- | :--- | :--- |
| **Cảm biến DHT22** | Input | Đo nhiệt độ (-40 đến 80°C, sai số `0.5°C`) | Ổn định |
| **Vi điều khiển SoC**| Process | CPU 32-bit, tích hợp Wi-Fi/Bluetooth | Ổn định |
| **Rơ-le Omron 5V** | Output | Chịu tải tối đa 220V - 10A (Điều khiển bơm) | Ổn định |

---

## Lưu ý: Xử lý tràn RAM do tệp Nhật ký 
Tệp `system.log` phình to quá mức khi nạp vào bộ nhớ tạm sẽ gây **tràn RAM ** và treo hệ thống.

**Cách xử lý an toàn:**
1. **KHÔNG** dùng lệnh `rm` xóa file trực tiếp khi ứng dụng đang chạy.
2. Giải phóng dung lượng bằng cách ghi đè rỗng: `true > /home/pi/smart-farm/system.log`
