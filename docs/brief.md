# V-VoiceRide 1-Page Brief

## Dự Án

**V-VoiceRide** là MVP trợ lý đặt xe bằng giọng nói tiếng Việt. Người dùng có thể nói yêu cầu tự nhiên như "Đặt xe từ VinUni đến Bệnh viện Bạch Mai"; hệ thống sẽ trích xuất thông tin chuyến đi, hỏi lại khi thiếu dữ liệu, đọc lại nội dung đặt xe và chỉ tạo booking mock sau khi người dùng xác nhận rõ ràng.

## Vấn Đề

Ứng dụng gọi xe đã quen thuộc tại Việt Nam, nhưng quy trình đặt xe trên app vẫn có thể khó với người lớn tuổi, người khiếm thị hoặc người không tự tin khi dùng giao diện mobile nhiều bước. Họ có thể nhập sai địa điểm, bỏ sót thông tin xác nhận hoặc cần người khác hỗ trợ đặt xe. Giao diện giọng nói có hướng dẫn giúp giảm thao tác tay và làm quy trình đặt xe gần với một cuộc gọi hỗ trợ hơn.

## Người Dùng Mục Tiêu

- Người lớn tuổi hoặc người ít tự tin với công nghệ, có thể nói tiếng Việt nhưng gặp khó với app nhiều bước.
- Người khiếm thị cần phản hồi bằng giọng nói và phần xác nhận dễ đọc.
- Admin/evaluator cần xem booking và conversation logs để đánh giá hệ thống.

## Quyết Định MVP

**Go, nhưng thu hẹp phạm vi.** Nhóm sẽ xây dựng mobile web app mô phỏng đặt xe, không làm hệ thống gọi xe thật.

## Tính Năng MVP

- Nhập yêu cầu bằng giọng nói và hiển thị transcript.
- Trích xuất intent tiếng Việt gồm điểm đón, điểm đến và loại xe.
- Hỏi lại khi thông tin thiếu hoặc mơ hồ.
- Phản hồi bằng cả text và voice.
- Bắt buộc xác nhận cuối trước khi booking.
- Tạo booking mock và hiển thị trạng thái.
- Admin dashboard để xem booking và conversation logs.

## Không Làm Trong MVP

- Điều phối tài xế thật.
- Thanh toán thật.
- Tối ưu bản đồ/routing đầy đủ.
- Tích hợp production với Grab, Be, Xanh SM hoặc nhà cung cấp gọi xe khác.

## Chỉ Số Thành Công

- Ít nhất 80% kịch bản test trích xuất đúng intent sau khi hỏi lại.
- 100% booking phải có xác nhận rõ ràng trước khi tạo.
- Người dùng hoàn thành happy path trong tối đa 3 phút.
- Admin xem được booking và transcript hội thoại tương ứng.

## Kết Quả Sau 6 Tuần

Đến demo day, nhóm cần có MVP web đã deploy, luồng đặt xe bằng giọng nói hoạt động, dashboard booking mock, bằng chứng evaluation, README, tài liệu kiến trúc, AI usage logs và video demo ngắn.
