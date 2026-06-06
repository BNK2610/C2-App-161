# V-VoiceRide PRD

## 1. Tổng Quan

V-VoiceRide là trợ lý giọng nói tiếng Việt cho quy trình đặt xe mô phỏng. Hệ thống giúp người dùng hoàn thành yêu cầu đặt xe thông qua giọng nói, hội thoại hỏi lại và xác nhận rõ ràng trước khi tạo booking mock.

## 2. Mục Tiêu

- Chứng minh rằng giao diện giọng nói tiếng Việt có thể hỗ trợ hoàn thành quy trình đặt xe một cách an toàn.
- Giảm thao tác nhập form cho người dùng gặp khó khăn với app gọi xe truyền thống.
- Hiển thị transcript và bước xác nhận để giảm rủi ro STT/LLM hiểu sai.
- Cho admin/evaluator xem booking và conversation logs để đánh giá.

## 3. Persona

**Người dùng chính:** Người lớn tuổi hoặc người ít tự tin với công nghệ, muốn đặt một chuyến xe đơn giản mà không phải thao tác nhiều màn hình.

**Người dùng cần hỗ trợ truy cập:** Người khiếm thị hoặc người cần hướng dẫn bằng giọng nói, đồng thời vẫn có transcript/xác nhận dạng text.

**Admin/evaluator:** Thành viên nhóm hoặc giảng viên cần xem booking, transcript, lỗi và kết quả evaluation.

## 4. Luồng Người Dùng Chính

1. Người dùng đăng nhập.
2. Người dùng mở trợ lý đặt xe.
3. Người dùng bấm micro và nói yêu cầu đặt xe.
4. Hệ thống chuyển giọng nói thành transcript.
5. LLM trích xuất điểm đón, điểm đến và loại xe.
6. Nếu thiếu thông tin, trợ lý hỏi thêm một câu cụ thể.
7. Trợ lý đọc/hiển thị lại tóm tắt chuyến đi.
8. Người dùng xác nhận hoặc yêu cầu đổi thông tin.
9. Hệ thống tạo booking mock và hiển thị trạng thái.
10. Admin có thể xem booking và conversation log.

## 5. Yêu Cầu Chức Năng

| ID | Yêu cầu | Mức độ |
|---|---|---|
| FR-01 | Người dùng có thể gửi yêu cầu đặt xe bằng voice hoặc text fallback. | Must |
| FR-02 | Hệ thống hiển thị transcript trước khi tiếp tục xử lý. | Must |
| FR-03 | Hệ thống trích xuất điểm đón, điểm đến và loại xe. | Must |
| FR-04 | Hệ thống hỏi lại khi thiếu trường bắt buộc. | Must |
| FR-05 | Hệ thống hỗ trợ ít nhất hai loại xe: xe máy và ô tô. | Must |
| FR-06 | Hệ thống đọc hoặc hiển thị xác nhận cuối trước khi booking. | Must |
| FR-07 | Hệ thống chỉ tạo booking mock sau khi người dùng xác nhận rõ ràng. | Must |
| FR-08 | Người dùng có thể huỷ hoặc sửa thông tin trước khi xác nhận. | Must |
| FR-09 | Admin có thể xem booking và conversation logs. | Should |
| FR-10 | Hệ thống lưu metadata evaluation như transcript, slot đã trích xuất và kết quả. | Should |

## 6. Yêu Cầu Phi Chức Năng

- UI phải dùng tốt trên màn hình mobile.
- Thông tin quan trọng của chuyến đi phải hiển thị bằng text, không chỉ đọc bằng voice.
- LLM temperature nên thấp để kết quả trích xuất ổn định.
- API cần có health/status endpoints để kiểm tra khi deploy.
- MVP không xử lý thanh toán thật, thông tin tài chính cá nhân hoặc điều phối tài xế thật.

## 7. Data Model Nháp

**Booking**

- `id`
- `user_id`
- `pickup`
- `destination`
- `vehicle_type`
- `status`: `draft`, `confirmed`, `mock_driver_assigned`, `completed`, `cancelled`
- `created_at`

**ConversationLog**

- `id`
- `booking_id`
- `role`: `user`, `assistant`, `system`
- `content`
- `transcript_source`: `voice`, `text`, `tts`
- `created_at`

**IntentExtraction**

- `pickup`
- `destination`
- `vehicle_type`
- `missing_fields`
- `confidence`
- `needs_confirmation`

## 8. Tiêu Chí Chấp Nhận

- Với câu "Đặt xe từ VinUni đến Bệnh viện Bạch Mai", hệ thống trích xuất đúng điểm đón và điểm đến, sau đó hỏi loại xe nếu còn thiếu.
- Với câu "Tôi muốn đi ô tô từ nhà đến chợ", hệ thống trích xuất loại xe là ô tô và hỏi lại nếu "nhà" hoặc "chợ" chưa đủ rõ.
- Khi đã có tóm tắt chuyến đi đầy đủ, hệ thống không tạo booking cho đến khi người dùng xác nhận rõ ràng.
- Với câu "Không, đổi điểm đến sang Việt Đức", hệ thống cập nhật destination trong draft booking và đọc lại phần xác nhận.
- Admin dashboard hiển thị tối thiểu booking ID, điểm đón, điểm đến, loại xe, trạng thái và transcript.

## 9. Rủi Ro

- STT có thể nghe sai địa danh tiếng Việt hoặc tên riêng.
- LLM có thể tự suy diễn trường còn thiếu.
- Voice API có thể hoạt động khác nhau giữa các trình duyệt.
- Demo phụ thuộc vào mạng và API keys.

Hướng giảm thiểu: luôn hiển thị transcript, bắt buộc xác nhận cuối, có text fallback và chuẩn bị bộ kịch bản evaluation cố định.
