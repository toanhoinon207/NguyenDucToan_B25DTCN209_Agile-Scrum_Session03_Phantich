# Phần 1 - Đề xuất

## Chiến lược 1

- **Feature 1:** Xử lý yêu cầu hủy chuyến
- **Feature 2:** Tính phí hủy chuyến
- **Feature 3:** Tính lại giá cho khách còn lại
- **Feature 4:** Gửi thông báo giá mới

## Chiến lược 2

- **Feature 1:** Hủy chuyến trước khi tài xế nhận chuyến - miễn phí
- **Feature 2:** Hủy chuyến sau khi tài xế nhận chuyến - phí 10.000đ
- **Feature 3:** Hủy chuyến thành công - tính lại giá và thông báo cho khách còn lại

# Phần 2 - So sánh

| Tiêu chí | Chiến lược 1 | Chiến lược 2 |
|---|---|---|
| Independent | Các chức năng phụ thuộc vào nhau, tính phí và thông báo cần kết quả hủy chuyến và giá mới | Mỗi luồng thể hiện một tình huống nghiệp vụ tương đối hoàn chỉnh, dễ xác định phụ thuộc |
| Small | Chia thành các chức năng nhỏ, phạm vi từng phần dễ xác định | Một luồng có thể bao gồm nhiều xử lý như hủy, tính phí, tính lại giá và thông báo |
| Valuable | Một chức năng riêng lẻ như tính phí chưa chắc mang lại giá trị sử dụng độc lập | Mỗi luồng giải quyết một nhu cầu cụ thể của khách hàng và có thể kiểm thử theo kết quả nghiệp vụ |

# Phần 3 - Lựa chon & đặc tả

- Lựa chọn chiến lược 2 vì mỗi User Story thể hiện một tình huống hủy chuyến có kết quả nghiệp vụ rõ ràng. Đội dễ kiểm thử quy tắc tính phí và đảm bảo quyền lợi của các khách còn lại.

## User Story

- Là khách hàng đặt xe ghép, tôi muốn hủy chuyến và được tính phí theo trạng thái nhận chuyến tại thời điểm máy chủ ghi nhận yêu cầu, để biết chính xác chi phí hủy.

## Kịch bản Given - When - Then

- **Given:** Khách đang ở trong chuyến ghép và yêu cầu hủy được gửi gần cùng thời điểm tài xế bấm nhận chuyến.

- **When:** Máy chủ ghi nhận yêu cầu hủy và xác định thứ tự xử lý sự kiện.

- **Then:** Nếu máy chủ ghi nhận tài xế nhận chuyến trước yêu cầu hủy, khách bị tính phí 10.000đ; nếu máy chủ ghi nhận yêu cầu hủy trước, khách được miễn phí. Sau khi hủy, hệ thống tính lại giá cho các khách còn lại và thông báo ngay giá mới.