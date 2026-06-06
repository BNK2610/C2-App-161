# AI20K-244 — V-VoiceRide Project Package

> **Tên đề tài:** AI Trợ Lý Tích Hợp Đặt Xe Qua Trợ Lý Giọng Nói Tiếng Việt  
> **Tên rút gọn đề xuất:** V-VoiceRide  
> **Nhóm:** 3 thành viên, cùng background AI  
> **Mục tiêu tài liệu:** Tổng hợp toàn bộ phần đã phân tích, survey/secondary research, Brief, PRD, UI Flow/Wireframe, GitHub setup, User Stories, kế hoạch 6 tuần và checklist triển khai để nhóm có thể bắt đầu Sprint 0/Tuần 1.

---

## Mục lục

1. [Cách dùng tài liệu này](#1-cách-dùng-tài-liệu-này)
2. [Tóm tắt đề tài](#2-tóm-tắt-đề-tài)
3. [Secondary Research / Public Survey Evidence](#3-secondary-research--public-survey-evidence)
4. [Kết luận từ khảo sát công khai để chốt MVP](#4-kết-luận-từ-khảo-sát-công-khai-để-chốt-mvp)
5. [1-Page Brief](#5-1-page-brief)
6. [Project Charter hoàn chỉnh](#6-project-charter-hoàn-chỉnh)
7. [PRD — Product Requirements Document](#7-prd--product-requirements-document)
8. [User Stories chi tiết](#8-user-stories-chi-tiết)
9. [Phân việc theo task cho nhóm 3 người](#9-phân-việc-theo-task-cho-nhóm-3-người)
10. [Roadmap 6 tuần](#10-roadmap-6-tuần)
11. [Wireframe / UI Flow](#11-wireframe--ui-flow)
12. [GitHub Repo Setup](#12-github-repo-setup)
13. [Survey riêng nhóm nên làm](#13-survey-riêng-nhóm-nên-làm)
14. [Evaluation Plan](#14-evaluation-plan)
15. [Risk & Mitigation](#15-risk--mitigation)
16. [Checklist hoàn thành Sprint 0 / Tuần 1](#16-checklist-hoàn-thành-sprint-0--tuần-1)
17. [Tài liệu tham khảo](#17-tài-liệu-tham-khảo)

---

# 1. Cách dùng tài liệu này

Tài liệu này được thiết kế để bạn có thể tách ra thành nhiều file nhỏ trong repo:

```text
repo/
├── docs/
│   ├── brief.md
│   ├── project-charter.md
│   ├── prd.md
│   ├── user-stories.md
│   ├── architecture.md
│   ├── ui-flow.md
│   ├── evaluation-plan.md
│   └── survey-plan.md
├── prompts/
│   ├── intent_extraction_prompt.md
│   └── dialogue_prompt.md
└── README.md
```

Bạn có thể dùng tài liệu này theo 4 deliverables bạn cần nộp:

| Deliverable | Phần nên lấy từ tài liệu này |
|---|---|
| Brief | Phần 5 |
| PRD | Phần 7 |
| Wireframe/UI Flow | Phần 11 |
| GitHub Repo | Phần 12 |

---

# 2. Tóm tắt đề tài

## 2.1. Mô tả ngắn

**V-VoiceRide** là một web/mobile web app hỗ trợ đặt xe mô phỏng bằng giọng nói tiếng Việt. Người dùng có thể nói yêu cầu đặt xe tự nhiên như:

- “Đặt xe từ VinUni đến Bệnh viện Bạch Mai.”
- “Tôi muốn đi từ nhà đến chợ.”
- “Đặt ô tô đến bệnh viện.”
- “Không, đổi điểm đến sang Việt Đức.”

Hệ thống sẽ:

1. Chuyển giọng nói thành văn bản.
2. Dùng AI để trích xuất điểm đón, điểm đến, loại xe.
3. Hỏi lại khi thiếu hoặc mơ hồ thông tin.
4. Đọc lại thông tin chuyến đi bằng giọng nói.
5. Chỉ tạo booking mock sau khi người dùng xác nhận rõ ràng.
6. Cho admin xem booking và conversation logs để đánh giá hệ thống.

## 2.2. Định vị MVP

MVP không phải là một ứng dụng gọi xe thật như Grab/Be/Xanh SM. MVP là một **voice booking assistant mô phỏng** để chứng minh rằng giao diện giọng nói tiếng Việt có thể giúp người dùng khó thao tác app hoàn thành quy trình đặt xe an toàn hơn.

## 2.3. Quyết định sản phẩm

```text
Decision: Go, nhưng làm MVP thu hẹp.

Scope chính:
- Web/mobile web app.
- Login + user/admin role.
- Voice booking flow.
- STT + LLM intent extraction + TTS.
- Hỏi lại khi thiếu thông tin.
- Xác nhận bắt buộc trước booking.
- Booking mock.
- Admin dashboard.
- Deploy online.
```

---

# 3. Secondary Research / Public Survey Evidence

> Lưu ý: Các nguồn dưới đây là **secondary evidence**. Chúng giúp chứng minh bài toán có cơ sở, nhưng nhóm vẫn nên làm khảo sát/phỏng vấn riêng để xác thực với bối cảnh Việt Nam và MVP cụ thể.

## 3.1. Rakuten Insight — Ride-hailing ở Việt Nam đã phổ biến

**Nguồn:** Rakuten Insight, “2025 Ride-Hailing App Landscape in Vietnam”  
**Ý nghĩa với dự án:** Dùng để chứng minh thị trường gọi xe công nghệ tại Việt Nam đủ phổ biến, không cần mất nhiều thời gian chứng minh “người Việt có dùng app đặt xe không”. Vấn đề cần tập trung là: **nhóm nào đang gặp khó khi thao tác app và voice có giúp họ không?**

Các điểm có thể dùng:

- Khảo sát về thị trường ride-hailing tại Việt Nam năm 2025.
- Grab là thương hiệu được sử dụng nhiều nhất trong khảo sát, Xanh SM đứng sau và Be chiếm thị phần nhỏ hơn.
- Dịch vụ gọi xe được dùng ở các thành phố lớn và cả khu vực ngoài các thành phố lớn.

**Hàm ý MVP:**

- MVP nên đặt trong bối cảnh đô thị Việt Nam.
- Nên hỗ trợ ít nhất 2 loại xe: xe máy và ô tô.
- Không nên làm quá nhiều loại xe trong MVP.
- Cần tập trung vào pain point thao tác app, không phải chứng minh thị trường gọi xe có tồn tại.

---

## 3.2. Grab AI Voice Assistant — case rất sát đề tài

**Nguồn:** Grab Product Team, “Grab’s AI Voice Assistant lets visually impaired users book rides with ease”  
**Ý nghĩa với dự án:** Đây là case rất gần với đề tài. Grab thử nghiệm AI Voice Assistant cho người khiếm thị, giúp họ đặt xe bằng voice command và được hướng dẫn qua quy trình booking.

Các điểm có thể dùng:

- Grab định vị tính năng này cho các nhóm underserved communities như người khuyết tật, người lớn tuổi và người ít quen công nghệ.
- Tính năng dùng AI/LLM và voice recognition để tương tác qua voice commands.
- Trợ lý hướng dẫn người dùng trong quá trình đặt xe.
- Trợ lý cập nhật trạng thái tài xế từ lúc tìm được tài xế đến khi tài xế đến nơi.
- Tính năng có các capability như hủy chuyến, gọi tài xế, đổi phương thức thanh toán.

**Hàm ý MVP:**

- Voice assistant cho booking là hướng có cơ sở thực tế.
- MVP cần có hội thoại nhiều lượt, không chỉ nhận lệnh một lần.
- MVP cần có xác nhận cuối trước booking.
- MVP nên có booking status mock.
- MVP nên có voice + text feedback, không chỉ text.

---

## 3.3. Grab fine-tune STT với local voice samples

**Nguồn:** Frontier Enterprise, “Grab powers on AI Centre of Excellence”  
**Ý nghĩa với dự án:** Case này cho thấy bài toán voice assistant không chỉ là gọi API STT, mà cần kiểm tra giọng địa phương, tên địa điểm và điểm quan tâm.

Điểm quan trọng:

- Grab fine-tune speech-to-text model với khoảng 80.000 local voice samples và tên các points of interest.
- Recognition cho Singaporean accents và building names tăng từ 46% lên 89%.

**Hàm ý MVP:**

- Nhóm cần test STT tiếng Việt với địa danh Việt Nam.
- Cần chuẩn bị bộ câu lệnh giọng nói riêng cho evaluation.
- Cần hiển thị transcript để người dùng kiểm tra hệ thống nghe đúng chưa.
- Cần luôn đọc lại/xác nhận thông tin trước booking để giảm rủi ro STT sai.

---

## 3.4. Mineta Transportation Institute — người lớn tuổi và ride-hailing

**Nguồn:** Mineta Transportation Institute, “Will Ride-Hailing Enhance Mobility for Older Adults? A California Survey”  
**Ý nghĩa với dự án:** Nghiên cứu này khảo sát người từ 55 tuổi trở lên ở California để xem họ dùng ride-hailing thế nào và các tính năng nào giúp cải thiện accessibility/safety/payment.

Các điểm có thể dùng:

- Khảo sát có 2.917 người từ 55 tuổi trở lên.
- Trong nhóm từ 65 tuổi trở lên, 44% từng trải nghiệm ride-hailing.
- 27% từng tự đặt chuyến qua điện thoại hoặc app.
- Các tính năng được nhiều người lớn tuổi quan tâm gồm tài xế được đào tạo hỗ trợ người lớn tuổi và phương thức thanh toán không cần liên kết tài khoản ngân hàng/thẻ tín dụng.

**Hàm ý MVP:**

- Persona người lớn tuổi/ít quen công nghệ là hợp lý.
- Nên có flow đơn giản, ít lựa chọn.
- Nên cân nhắc caregiver/admin mode hoặc người thân hỗ trợ.
- Không nên đưa thanh toán thật vào MVP.
- Nên mô phỏng booking thay vì xử lý tiền thật.

---

## 3.5. Research về người lớn tuổi dùng ride-hailing booking technology

**Nguồn:** Misra et al., “How Older Adults Use Ride-hailing Booking Technology in California”  
**Ý nghĩa với dự án:** Nghiên cứu phân tích cách người lớn tuổi đặt chuyến ride-hailing: tự đặt qua app, tự đặt qua phone, được người thân/caregiver đặt hộ, hoặc đi cùng người đặt hộ.

Các điểm có thể dùng:

- Ride-hailing có tiềm năng cải thiện mobility cho người lớn tuổi, đặc biệt người không thể hoặc không muốn tự lái.
- Người tự tin hơn với công nghệ có xu hướng tự đặt qua app.
- Người thận trọng/ít thoải mái với công nghệ có xu hướng dùng phone booking hoặc nhờ người khác.

**Hàm ý MVP:**

- Voice booking có thể là cầu nối giữa app và phone booking.
- Người dùng mục tiêu không nhất thiết không có smartphone; vấn đề là họ không tự tin khi thao tác app.
- MVP nên giảm thao tác bằng tay và tăng hướng dẫn bằng giọng nói.

---

## 3.6. Uber Senior Accounts / Simple Mode

**Nguồn:** Axios/The Verge coverage về Uber Senior Accounts và Simple Mode  
**Ý nghĩa với dự án:** Uber đã triển khai hướng tiếp cận riêng cho người lớn tuổi: giao diện đơn giản, chữ lớn, ít nút, saved destinations và family/caregiver support.

Các điểm có thể dùng:

- Senior accounts giúp người lớn tuổi tiếp cận dịch vụ gọi xe dễ hơn.
- Simple Mode tập trung vào giao diện đơn giản, ít nút, chữ lớn.
- Family profile/caregiver support giúp người thân hỗ trợ quản lý/chọn chuyến.
- Saved destinations giúp giảm thao tác nhập địa chỉ.

**Hàm ý MVP:**

- UI nên có chữ lớn, nút lớn, ít bước.
- Nên có saved places nếu còn thời gian.
- Nên có admin/caregiver concept ở mức mock.
- Không nên xây UI dày đặc như app gọi xe đầy đủ.

---

## 3.7. AARP — người trên 50 tuổi dùng công nghệ nhiều hơn nhưng vẫn cần thiết kế phù hợp

**Nguồn:** AARP Tech Trends and Older Adults  
**Ý nghĩa với dự án:** Người lớn tuổi ngày càng dùng smartphone và dịch vụ số, nhưng vẫn có rào cản về usability, niềm tin và độ tự tin.

Các điểm có thể dùng:

- Smartphone ownership của nhóm 50+ tăng mạnh qua các năm.
- Người trên 50 tuổi vẫn có sự thận trọng với AI và dữ liệu cá nhân.
- Thiết kế sản phẩm cần chú ý usability, privacy, confidence và hướng dẫn rõ ràng.

**Hàm ý MVP:**

- Không nên giả định người lớn tuổi không dùng công nghệ.
- Vấn đề chính là thiết kế luồng dễ hiểu, đáng tin, ít rủi ro.
- Cần giải thích rõ AI đang làm gì và luôn cho người dùng quyền xác nhận/hủy.

---

# 4. Kết luận từ khảo sát công khai để chốt MVP

## 4.1. Những điều secondary research đã hỗ trợ

Các nguồn công khai cho thấy:

1. **Ride-hailing đã phổ biến tại Việt Nam**, nên bài toán có bối cảnh thực tế.
2. **Voice assistant cho đặt xe đã có tiền lệ thực tế** qua case Grab AI Voice Assistant.
3. **Người lớn tuổi có nhu cầu mobility**, nhưng có thể gặp rào cản công nghệ.
4. **Nhóm người không tự tin công nghệ có xu hướng cần hỗ trợ hoặc dùng phone booking**, nên voice interface là hướng đáng thử.
5. **Simple Mode, saved places, caregiver support** là các pattern phù hợp với người lớn tuổi.
6. **STT có rủi ro lớn với accent/tên địa điểm**, nên MVP cần transcript + confirmation guardrail.

## 4.2. Những điều secondary research chưa trả lời

Các nguồn công khai chưa trả lời trực tiếp các câu hỏi sau trong bối cảnh Việt Nam:

1. Người dùng Việt Nam kẹt nhất ở bước nào khi đặt xe?
2. Người lớn tuổi Việt Nam có muốn dùng voice để đặt xe không?
3. Họ sợ nhất điều gì: sai điểm đón, sai điểm đến, sai giá, không tìm thấy tài xế, thanh toán?
4. Họ muốn xác nhận bằng giọng nói hay nút bấm?
5. Câu lệnh tiếng Việt tự nhiên họ sẽ nói là gì?
6. Họ có tin AI đọc lại thông tin và đặt hộ không?

Vì vậy, nhóm vẫn nên làm khảo sát/phỏng vấn riêng.

## 4.3. Quyết định MVP sau research

```text
MVP nên làm:
- Mobile web app.
- Voice booking bằng tiếng Việt.
- Booking mock, không đặt xe thật.
- Hỏi lại khi thiếu thông tin.
- Đọc lại thông tin chuyến đi.
- Bắt buộc xác nhận trước booking.
- UI chữ lớn/nút lớn.
- Admin xem log để evaluation.

MVP chưa nên làm:
- Thanh toán thật.
- API đặt xe thật.
- GPS tracking thật.
- Native app.
- Agent tự chủ hoàn toàn.
```

---

# 5. 1-Page Brief

## 5.1. Problem

Một số nhóm người dùng như người lớn tuổi, người khiếm thị, người thị lực kém hoặc người không quen thao tác ứng dụng gặp khó khăn khi đặt xe công nghệ vì quy trình hiện tại yêu cầu nhiều thao tác trên màn hình: nhập điểm đón, nhập điểm đến, chọn loại xe, đọc giá, xác nhận chuyến và theo dõi tài xế.

Hiện tại, họ thường phải nhờ người khác đặt xe hộ, gọi taxi truyền thống hoặc tự thao tác chậm và dễ nhầm lẫn. Điều này làm giảm khả năng di chuyển độc lập và tạo rào cản tiếp cận dịch vụ gọi xe hiện đại.

## 5.2. Target Users

Người dùng chính của MVP là người lớn tuổi hoặc người ít quen sử dụng app đặt xe, nhưng vẫn có nhu cầu di chuyển độc lập trong thành phố.

Người dùng phụ là admin/người hỗ trợ, có thể xem booking mô phỏng và log hội thoại để kiểm tra hệ thống hoạt động đúng hay không.

## 5.3. Proposed Solution

Xây dựng một web/mobile web app cho phép người dùng đặt xe mô phỏng bằng giọng nói tiếng Việt. Người dùng có thể nói yêu cầu tự nhiên như:

- “Đặt xe từ VinUni đến Bệnh viện Bạch Mai.”
- “Tôi muốn đi từ nhà đến chợ.”
- “Đặt ô tô đến bệnh viện.”
- “Không, đổi điểm đến sang Việt Đức.”

Hệ thống sẽ chuyển giọng nói thành văn bản, dùng AI để trích xuất thông tin đặt xe, hỏi lại nếu thiếu thông tin, đọc lại thông tin chuyến đi và chỉ tạo booking mock sau khi người dùng xác nhận rõ ràng.

## 5.4. MVP Scope

Trong 6 tuần, MVP sẽ gồm:

- Đăng ký, đăng nhập.
- Phân quyền user/admin.
- Giao diện mobile web.
- Nút micro để nhập lệnh bằng giọng nói.
- STT tiếng Việt.
- AI trích xuất điểm đón, điểm đến, loại xe.
- AI hỏi lại khi thiếu thông tin.
- TTS đọc lại thông tin chuyến đi.
- Bắt buộc xác nhận trước khi tạo booking.
- Booking mock.
- Booking status mock.
- Admin dashboard xem user, booking và conversation logs.
- Deploy online có URL truy cập.

## 5.5. Out-of-scope

MVP chưa làm:

- Không tích hợp đặt xe thật với Grab, Be, Xanh SM hoặc taxi thật.
- Không thanh toán thật.
- Không tracking GPS tài xế thật.
- Không gọi tài xế thật.
- Không làm native mobile app.
- Không cho AI tự động đặt xe nếu người dùng chưa xác nhận.
- Không xử lý mọi địa chỉ phức tạp hoặc mọi giọng vùng miền ở mức hoàn hảo.

## 5.6. Success Metrics

Dự án được xem là thành công nếu:

- Có web/mobile web app deploy online.
- Có login và phân quyền user/admin.
- Người dùng có thể hoàn thành flow đặt xe mô phỏng bằng giọng nói.
- Ít nhất 80% test cases trích xuất đúng điểm đón, điểm đến và loại xe.
- Ít nhất 90% case thiếu thông tin được AI hỏi lại đúng.
- 100% booking mock phải có bước xác nhận cuối.
- Có 30–50 test cases để đánh giá.
- Có user testing nhỏ với tối thiểu 5 người.

---

# 6. Project Charter hoàn chỉnh

## 6.1. Tên dự án

**V-VoiceRide: AI Trợ Lý Đặt Xe Bằng Giọng Nói Tiếng Việt**

## 6.2. Mô tả dự án

V-VoiceRide là một ứng dụng web/mobile web hỗ trợ đặt xe mô phỏng bằng giọng nói tiếng Việt. Ứng dụng hướng đến người dùng gặp khó khăn khi thao tác app đặt xe truyền thống, đặc biệt là người lớn tuổi, người thị lực kém, người khiếm thị hoặc người ít quen công nghệ.

Hệ thống cho phép người dùng nói yêu cầu đặt xe, hiểu ý định, hỏi lại khi thiếu thông tin, đọc lại thông tin chuyến đi và chỉ tạo booking mock sau khi người dùng xác nhận.

## 6.3. Problem Statement

Người lớn tuổi, người khiếm thị hoặc người không quen thao tác ứng dụng gặp khó khăn khi đặt xe công nghệ vì quy trình hiện tại yêu cầu nhiều thao tác trên màn hình như nhập địa chỉ, chọn loại xe, đọc giá, xác nhận chuyến và theo dõi tài xế. Hiện họ thường phải nhờ người khác đặt hộ, gọi taxi truyền thống hoặc tự thao tác chậm và dễ nhầm lẫn. Điều này làm giảm tính chủ động trong di chuyển và tạo rào cản tiếp cận dịch vụ gọi xe hiện đại.

## 6.4. Target Users

### Primary User

Người lớn tuổi hoặc người ít quen thao tác ứng dụng đặt xe, nhưng vẫn có nhu cầu di chuyển độc lập trong thành phố.

### Secondary User

Admin hoặc người hỗ trợ, có thể xem booking mock và log hội thoại để đánh giá hệ thống.

## 6.5. SMART Goal

Trong 6 tuần, nhóm xây dựng một web/mobile web app hỗ trợ đặt xe mô phỏng bằng giọng nói tiếng Việt. Hệ thống cho phép user đăng nhập, nói yêu cầu đặt xe, được AI hỏi lại khi thiếu thông tin, nghe AI đọc lại thông tin chuyến đi, xác nhận bằng giọng nói hoặc nút bấm, và tạo booking mock. Sản phẩm có role user/admin, admin dashboard, được deploy online, có test cases và báo cáo evaluation.

## 6.6. In-scope

- Web/mobile web responsive.
- Đăng ký/đăng nhập.
- Phân quyền user/admin.
- Voice input.
- STT tiếng Việt.
- Transcript display.
- LLM intent extraction.
- Dialogue manager.
- Hỏi lại khi thiếu thông tin.
- TTS đọc lại thông tin chuyến đi.
- Confirmation guardrail.
- Booking mock.
- Booking status mock.
- Admin dashboard.
- Conversation logs.
- Evaluation test cases.
- User testing nhỏ.
- Deploy online.

## 6.7. Out-of-scope

- Không đặt xe thật.
- Không thanh toán thật.
- Không tracking GPS tài xế thật.
- Không gọi tài xế thật.
- Không native Android/iOS app.
- Không điều phối tài xế thật.
- Không hỗ trợ mọi địa chỉ phức tạp.
- Không cho AI tự ý tạo booking nếu chưa xác nhận.
- Không xử lý tình huống khẩn cấp.

## 6.8. Success Metrics

| Nhóm | Metric | Target |
|---|---|---:|
| Product | Tỷ lệ hoàn thành booking mock trong test case chuẩn | ≥ 80% |
| Product | Người test hiểu flow sau một lần hướng dẫn | ≥ 80% |
| Product | Thời gian hoàn thành booking mock | < 2 phút |
| AI | Trích xuất đúng pickup/dropoff/vehicle_type | ≥ 80% |
| AI | Hỏi lại đúng khi thiếu thông tin | ≥ 90% |
| Safety | Booking có xác nhận cuối | 100% |
| Engineering | App deploy online | Có |
| Engineering | Login + role user/admin | Có |
| Evaluation | Số test cases | 30–50 |
| Validation | Số người user testing | ≥ 5 |

## 6.9. Stakeholders

| Stakeholder | Vai trò | Cần nhận gì |
|---|---|---|
| Mentor | Góp ý scope, đánh giá hướng đi | Brief, PRD, demo, evaluation |
| Người dùng thử | Phản hồi usability | Prototype/demo |
| Nhóm phát triển | Thực thi dự án | Task board, PRD, API spec |
| Admin demo | Kiểm tra log và booking | Admin dashboard |

## 6.10. Final Demo

Demo cuối kỳ sẽ thể hiện luồng:

1. User đăng nhập.
2. User bấm micro.
3. User nói yêu cầu đặt xe.
4. AI hỏi lại nếu thiếu thông tin.
5. AI đọc lại thông tin chuyến đi.
6. User xác nhận.
7. Hệ thống tạo booking mock.
8. User xem booking status.
9. Admin xem booking và conversation logs.

---

# 7. PRD — Product Requirements Document

## 7.1. Overview

V-VoiceRide là web/mobile web app hỗ trợ đặt xe mô phỏng bằng giọng nói tiếng Việt. Hệ thống tập trung vào nhóm người dùng gặp khó khăn khi thao tác app đặt xe truyền thống. MVP không đặt xe thật, mà mô phỏng quy trình booking để kiểm chứng voice-first workflow.

## 7.2. Goals

- Cho phép người dùng đặt xe mock bằng giọng nói.
- Giảm thao tác nhập địa chỉ/loại xe bằng tay.
- Đảm bảo AI hỏi lại khi thiếu thông tin.
- Đảm bảo AI không tự ý tạo booking nếu chưa xác nhận.
- Tạo admin dashboard để phục vụ evaluation.
- Deploy online để mentor/user test truy cập được.

## 7.3. Non-goals

- Không tích hợp API hãng xe thật.
- Không xử lý thanh toán.
- Không tracking GPS thật.
- Không tự động gọi tài xế.
- Không xây app native.
- Không tối ưu toàn bộ bài toán map/geocoding.

## 7.4. Main User Flow

```text
Login
  ↓
Home / Voice Button
  ↓
User speaks
  ↓
STT Transcript
  ↓
AI checks missing info
  ├── Missing info → Ask follow-up → User speaks again
  └── Enough info → Confirmation screen
                         ↓
                    User confirms
                         ↓
                   Booking created
                         ↓
                  Booking status
```

## 7.5. Functional Requirements

### FR-01: Authentication

- User có thể đăng ký.
- User có thể đăng nhập.
- Hệ thống có role user/admin.

### FR-02: Voice Input

- User có thể bấm nút micro.
- Hệ thống nhận audio.
- Hệ thống chuyển audio thành transcript.
- Transcript hiển thị trên UI.

### FR-03: Intent Extraction

Hệ thống trích xuất:

- `pickup`
- `dropoff`
- `vehicle_type`
- `missing_fields`
- `is_confirmation`
- `is_cancellation`

### FR-04: Dialogue Manager

Hệ thống có thể:

- Hỏi lại nếu thiếu pickup.
- Hỏi lại nếu thiếu dropoff.
- Hỏi lại nếu thiếu vehicle_type.
- Cập nhật thông tin khi user sửa.
- Hủy session nếu user yêu cầu hủy.
- Chuyển sang xác nhận khi đủ thông tin.

### FR-05: Confirmation Guardrail

- Không tạo booking nếu thiếu thông tin.
- Không tạo booking nếu user chưa xác nhận.
- Mọi booking phải có confirmation.

### FR-06: Mock Booking

Booking mock gồm:

- user_id
- pickup_address
- dropoff_address
- vehicle_type
- estimated_price
- status
- created_at

### FR-07: Admin Dashboard

Admin xem được:

- danh sách users,
- danh sách bookings,
- conversation logs,
- extracted intent JSON.

## 7.6. AI Workflow

Input cho AI:

- transcript hiện tại,
- dialogue state hiện tại,
- thông tin đã có trong session.

Output mong muốn:

```json
{
  "intent": "book_ride",
  "pickup": "VinUni",
  "dropoff": "Bệnh viện Bạch Mai",
  "vehicle_type": null,
  "missing_fields": ["vehicle_type"],
  "reply": "Bạn muốn đi xe máy hay ô tô?",
  "can_confirm": false,
  "is_confirmation": false,
  "is_cancellation": false
}
```

AI không được tạo booking trực tiếp. Backend chỉ tạo booking nếu:

- pickup không rỗng,
- dropoff không rỗng,
- vehicle_type không rỗng,
- user đã xác nhận.

---

# 8. User Stories chi tiết

## Epic 1: Authentication & User Management

### US-01: Đăng ký tài khoản

**User Story:**  
Với vai trò là người dùng mới, tôi muốn đăng ký tài khoản để sử dụng hệ thống đặt xe bằng giọng nói.

**Acceptance Criteria:**

- Người dùng nhập được tên, email/số điện thoại, mật khẩu.
- Hệ thống tạo tài khoản mới.
- Không cho đăng ký trùng email/số điện thoại.
- Sau đăng ký, người dùng có thể đăng nhập.

**Priority:** Must-have

---

### US-02: Đăng nhập

**User Story:**  
Với vai trò là người dùng, tôi muốn đăng nhập để sử dụng tính năng đặt xe.

**Acceptance Criteria:**

- Người dùng đăng nhập bằng email/số điện thoại và mật khẩu.
- Nếu thông tin sai, hệ thống báo lỗi rõ ràng.
- Nếu đúng, chuyển đến màn hình đặt xe.
- Session/token được lưu.

**Priority:** Must-have

---

### US-03: Phân quyền user/admin

**User Story:**  
Với vai trò là hệ thống, tôi muốn phân biệt user và admin để mỗi nhóm chỉ truy cập chức năng phù hợp.

**Acceptance Criteria:**

- User chỉ thấy giao diện đặt xe và booking của mình.
- Admin thấy dashboard quản trị.
- User không truy cập được admin dashboard.
- Admin xem được booking/log toàn hệ thống.

**Priority:** Must-have

---

## Epic 2: Voice Booking Core Flow

### US-04: Bắt đầu đặt xe bằng giọng nói

**User Story:**  
Với vai trò là người dùng, tôi muốn bấm nút micro và nói yêu cầu đặt xe để không phải nhập địa chỉ thủ công.

**Acceptance Criteria:**

- Có nút micro lớn.
- Khi bấm micro, hệ thống hiển thị trạng thái đang nghe.
- Người dùng nói được câu lệnh tiếng Việt.
- Audio được chuyển sang bước xử lý.

**Priority:** Must-have

---

### US-05: Chuyển giọng nói thành văn bản

**User Story:**  
Với vai trò là người dùng, tôi muốn hệ thống hiển thị lại nội dung đã nghe để biết hệ thống có nghe đúng không.

**Acceptance Criteria:**

- Audio được chuyển thành text.
- Transcript hiển thị trên giao diện.
- Nếu STT lỗi, hệ thống báo thử lại.
- Transcript được lưu vào conversation log.

**Priority:** Must-have

---

### US-06: Trích xuất thông tin đặt xe

**User Story:**  
Với vai trò là người dùng, tôi muốn hệ thống hiểu điểm đón, điểm đến và loại xe từ câu nói tự nhiên.

**Acceptance Criteria:**

- Trích xuất được pickup nếu có.
- Trích xuất được dropoff nếu có.
- Trích xuất được vehicle_type nếu có.
- Output chuẩn JSON.
- Nếu thiếu field, đánh dấu missing_fields.

**Priority:** Must-have

---

### US-07: Hỏi lại khi thiếu điểm đón

**User Story:**  
Với vai trò là người dùng, nếu tôi chưa nói điểm đón, tôi muốn hệ thống hỏi lại.

**Acceptance Criteria:**

- Nếu pickup rỗng, hệ thống hỏi: “Bạn muốn được đón ở đâu?”
- Câu trả lời tiếp theo cập nhật pickup.
- Không tạo booking khi thiếu pickup.

**Priority:** Must-have

---

### US-08: Hỏi lại khi thiếu điểm đến

**User Story:**  
Với vai trò là người dùng, nếu tôi chưa nói điểm đến, tôi muốn hệ thống hỏi lại để tránh đặt sai chuyến.

**Acceptance Criteria:**

- Nếu dropoff rỗng, hệ thống hỏi: “Bạn muốn đi đến đâu?”
- Câu trả lời tiếp theo cập nhật dropoff.
- Không tạo booking khi thiếu dropoff.

**Priority:** Must-have

---

### US-09: Hỏi lại khi thiếu loại xe

**User Story:**  
Với vai trò là người dùng, nếu tôi chưa chọn loại xe, tôi muốn hệ thống hỏi tôi muốn đi xe máy hay ô tô.

**Acceptance Criteria:**

- Nếu vehicle_type rỗng, hệ thống hỏi loại xe.
- Hỗ trợ ít nhất xe máy và ô tô.
- User có thể trả lời bằng giọng nói.
- Hệ thống cập nhật vehicle_type.

**Priority:** Must-have

---

### US-10: Đọc lại thông tin chuyến đi trước khi đặt

**User Story:**  
Với vai trò là người dùng, tôi muốn hệ thống đọc lại thông tin chuyến đi để kiểm tra trước khi xác nhận.

**Acceptance Criteria:**

- Khi đủ pickup, dropoff, vehicle_type, hệ thống tạo câu xác nhận.
- Câu xác nhận gồm điểm đón, điểm đến, loại xe, giá ước tính mock.
- Câu xác nhận hiển thị bằng text.
- Câu xác nhận được đọc bằng TTS.

**Priority:** Must-have

---

### US-11: Xác nhận đặt xe

**User Story:**  
Với vai trò là người dùng, tôi muốn xác nhận bằng giọng nói hoặc nút bấm trước khi hệ thống tạo booking.

**Acceptance Criteria:**

- User có thể nói “Xác nhận”, “Đúng rồi”, “Đặt xe”, “Ok”.
- User có thể bấm nút xác nhận.
- Hệ thống chỉ tạo booking sau xác nhận.
- Nếu user nói “không”, hệ thống không tạo booking.

**Priority:** Must-have

---

### US-12: Không tạo booking nếu chưa xác nhận

**User Story:**  
Với vai trò là người dùng, tôi muốn hệ thống không tự động đặt xe nếu tôi chưa xác nhận rõ ràng.

**Acceptance Criteria:**

- Nếu chưa có confirmation, không gọi API tạo booking.
- Nếu thiếu thông tin, không tạo booking.
- Nếu người dùng từ chối, không tạo booking.
- 100% booking phải có trạng thái confirmed.

**Priority:** Must-have

---

## Epic 3: Booking Mock

### US-13: Tạo booking mô phỏng

**User Story:**  
Với vai trò là người dùng, sau khi xác nhận, tôi muốn hệ thống tạo một chuyến đi mô phỏng để biết yêu cầu đã được ghi nhận.

**Acceptance Criteria:**

- Booking được lưu vào database.
- Booking có pickup, dropoff, vehicle_type, estimated_price, status.
- Status ban đầu là created hoặc finding_driver.
- User thấy thông báo booking thành công.

**Priority:** Must-have

---

### US-14: Xem trạng thái booking mô phỏng

**User Story:**  
Với vai trò là người dùng, tôi muốn xem trạng thái chuyến đi mô phỏng sau khi đặt.

**Acceptance Criteria:**

- User xem được trạng thái booking.
- Hỗ trợ ít nhất: đã tạo, đang tìm tài xế, đã có tài xế mô phỏng.
- Trạng thái hiển thị rõ trên UI.

**Priority:** Must-have

---

### US-15: Xem lịch sử booking của user

**User Story:**  
Với vai trò là người dùng, tôi muốn xem lại các chuyến đã đặt mô phỏng.

**Acceptance Criteria:**

- User xem được danh sách booking của mình.
- User không xem được booking của người khác.
- Mỗi booking hiển thị điểm đón, điểm đến, loại xe, trạng thái, thời gian.

**Priority:** Must-have

---

## Epic 4: Admin Dashboard

### US-16: Admin xem danh sách user

**User Story:**  
Với vai trò là admin, tôi muốn xem danh sách user để quản lý hệ thống demo.

**Acceptance Criteria:**

- Admin xem được danh sách user.
- Hiển thị tên, email/số điện thoại, role, thời gian tạo.
- User thường không truy cập được trang này.

**Priority:** Must-have

---

### US-17: Admin xem danh sách booking

**User Story:**  
Với vai trò là admin, tôi muốn xem danh sách booking để kiểm tra hệ thống xử lý đúng không.

**Acceptance Criteria:**

- Admin xem được toàn bộ booking.
- Hiển thị user, pickup, dropoff, vehicle_type, status.
- Có thể xem chi tiết từng booking nếu kịp.

**Priority:** Must-have

---

### US-18: Admin xem log hội thoại

**User Story:**  
Với vai trò là admin, tôi muốn xem transcript, phản hồi AI và intent được trích xuất để đánh giá chất lượng hệ thống.

**Acceptance Criteria:**

- Admin xem được user_input_text.
- Admin xem được ai_response_text.
- Admin xem được extracted_intent_json.
- Admin xem được dialogue_state.
- Log được lưu theo session.

**Priority:** Must-have

---

## Epic 5: Evaluation & Deployment

### US-19: Ghi log phục vụ evaluation

**User Story:**  
Với vai trò là nhóm phát triển, tôi muốn hệ thống lưu log để đánh giá lỗi STT, lỗi intent và lỗi hội thoại.

**Acceptance Criteria:**

- Mỗi lượt hội thoại được lưu.
- Có transcript.
- Có intent JSON.
- Có trạng thái.
- Có thông tin booking nếu đã tạo.

**Priority:** Must-have

---

### US-20: Deploy online

**User Story:**  
Với vai trò là mentor/người đánh giá, tôi muốn truy cập app qua URL để kiểm tra sản phẩm mà không cần chạy local.

**Acceptance Criteria:**

- Frontend deploy online.
- Backend deploy online.
- Database cloud hoặc remote hoạt động.
- Có tài khoản demo user/admin.
- README hướng dẫn truy cập.

**Priority:** Must-have

---

## User Stories nếu còn thời gian

### US-21: User lưu địa điểm quen thuộc

**Priority:** Should-have  
User có thể lưu Nhà, Bệnh viện, Chợ, Trường học để đặt xe nhanh hơn.

### US-22: Đặt xe bằng saved place

**Priority:** Should-have  
User nói “Đưa tôi về nhà” và hệ thống hiểu điểm đến là địa điểm đã lưu.

### US-23: Sửa điểm đến bằng giọng nói

**Priority:** Should-have  
User nói “Đổi điểm đến thành Bệnh viện Việt Đức” và hệ thống cập nhật dropoff.

### US-24: Sửa loại xe bằng giọng nói

**Priority:** Should-have  
User nói “Đổi sang xe máy” và hệ thống cập nhật vehicle_type.

### US-25: Hủy booking trước khi xác nhận

**Priority:** Should-have  
User nói “Hủy” hoặc “Tôi không đặt nữa” và hệ thống hủy session.

### US-26: Simple Mode nâng cao

**Priority:** Should-have  
Giao diện có font lớn, nút lớn, ít lựa chọn, hướng dẫn rõ.

### US-27: Voice-first flow

**Priority:** Could-have  
User có thể chọn loại xe, xác nhận, hủy, sửa thông tin bằng giọng nói.

### US-28: Hiển thị bản đồ đơn giản

**Priority:** Could-have  
Hiển thị điểm đón/điểm đến trên bản đồ hoặc mock map.

### US-29: Geocoding địa chỉ

**Priority:** Could-have  
Chuyển địa chỉ thành tọa độ bằng API hoặc mock resolver.

### US-30: Caregiver mode

**Priority:** Could-have  
Người thân/admin có thể xem booking hoặc tạo saved places cho user.

### US-31: Tài xế mô phỏng

**Priority:** Could-have  
Sau booking, hệ thống tạo tên tài xế, biển số, màu xe, ETA mock.

### US-32: Booking status tự động thay đổi

**Priority:** Could-have  
Status chuyển từ finding_driver sang driver_assigned rồi arriving.

---

# 9. Phân việc theo task cho nhóm 3 người

Vì cả 3 thành viên đều có background AI, không nên chia cứng thành một người AI, một người frontend, một người backend. Nên chia theo module/task package, mỗi module có output rõ ràng và review chéo.

## 9.1. Thành viên A — Dialogue Intelligence & Intent Quality

### Trách nhiệm chính

- Hiểu ý định đặt xe.
- Thiết kế prompt.
- Thiết kế dialogue state.
- Đảm bảo AI hỏi lại/xác nhận đúng.

### Task chi tiết

- Xây dựng intent schema.
- Viết prompt extraction.
- Viết prompt dialogue.
- Xử lý thiếu pickup/dropoff/vehicle_type.
- Xử lý xác nhận.
- Xử lý hủy.
- Xử lý sửa thông tin.
- Tạo test cases cho intent.
- Đánh giá AI output.

### Deliverables

- `prompts/intent_extraction_prompt.md`
- `prompts/dialogue_prompt.md`
- Intent JSON schema.
- Dialogue state design.
- 30–50 AI test cases.
- Evaluation note về lỗi AI.

## 9.2. Thành viên B — Speech Interaction & User Flow

### Trách nhiệm chính

- Voice interaction.
- UI flow.
- Trải nghiệm người dùng.
- STT/TTS integration.

### Task chi tiết

- Test STT tiếng Việt.
- Test TTS tiếng Việt.
- Tạo câu lệnh giọng nói thực tế.
- Thiết kế user flow.
- Vẽ wireframe.
- Làm voice UI.
- Hiển thị transcript.
- Làm confirmation screen.
- Làm booking status screen.
- Làm Simple Mode.
- Chạy user testing.

### Deliverables

- Wireframe/Figma.
- UI Flow.
- Voice UI.
- Transcript UI.
- Confirmation screen.
- Booking status screen.
- User testing summary.

## 9.3. Thành viên C — System, Booking Mock, Admin, Deploy & Evaluation

### Trách nhiệm chính

- Hệ thống backend/frontend integration.
- Auth.
- Booking mock.
- Admin dashboard.
- Deploy.
- Evaluation report.

### Task chi tiết

- Setup repo.
- Setup frontend/backend skeleton.
- Thiết kế database.
- Làm auth.
- Làm role user/admin.
- Làm API `/dialogue/message`.
- Làm API booking.
- Lưu conversation logs.
- Làm admin dashboard.
- Deploy.
- Viết README.
- Viết evaluation report.

### Deliverables

- GitHub repo.
- Backend API.
- Database schema.
- Auth + role.
- Booking mock service.
- Admin dashboard.
- Deploy URL.
- README.
- Evaluation report.

## 9.4. Review chéo

| Hạng mục | Người làm chính | Người review |
|---|---|---|
| Prompt intent extraction | A | B + C |
| STT test cases | B | A + C |
| Dialogue state | A | C |
| API output format | C | A + B |
| UX flow | B | A + C |
| Evaluation metrics | C | A + B |
| Demo script | B | A + C |

---

# 10. Roadmap 6 tuần

## Tuần 1 — Problem validation, Brief, PRD, Wireframe, Repo

### Mục tiêu

Chốt bài toán, chốt MVP, có tài liệu và nền tảng repo.

### Deliverables

- Brief.
- PRD.
- Wireframe/UI Flow.
- GitHub repo setup.
- Intent schema v1.
- Survey form.
- 30 câu lệnh test ban đầu.

### Task A

- Xác định intent chính.
- Thiết kế JSON schema.
- Viết prompt thử nghiệm.
- Tạo test câu lệnh.

### Task B

- Test STT/TTS sơ bộ.
- Vẽ user flow/wireframe.
- Làm survey form.

### Task C

- Tạo repo.
- Setup docs.
- Setup frontend/backend skeleton.
- Tạo task board.

## Tuần 2 — Text Booking End-to-End

### Mục tiêu

Hoàn thành luồng đặt xe bằng text.

### Deliverables

- Login.
- Text dialogue.
- Intent extraction.
- Missing information handling.
- Booking mock.
- Admin xem booking.

## Tuần 3 — Voice Integration & Checkpoint Demo

### Mục tiêu

Có demo đặt xe bằng giọng nói end-to-end.

### Deliverables

- STT.
- TTS.
- Voice input UI.
- Confirmation by voice/button.
- Demo URL.
- Video backup.

## Tuần 4 — Error Recovery & Saved Places

### Mục tiêu

Tăng chất lượng sản phẩm và xử lý các case thực tế hơn.

### Deliverables

- Sửa thông tin bằng giọng nói.
- Hủy session.
- Saved places nếu kịp.
- Evaluation set 30–50 cases.
- Admin log tốt hơn.

## Tuần 5 — Final Deploy, User Testing, Evaluation

### Mục tiêu

Đóng scope, deploy final, chạy test và user testing.

### Deliverables

- Final deployed app.
- Demo account.
- Evaluation report.
- User testing summary.
- README.

## Tuần 6 — Polish, Report, Slide, Rehearsal

### Mục tiêu

Hoàn thiện trình bày, không thêm tính năng lớn.

### Deliverables

- Final slide.
- Final report.
- Demo script.
- Video backup.
- Q&A document.
- Repo sạch.

---

# 11. Wireframe / UI Flow

## 11.1. Các màn hình bắt buộc

### Screen 1 — Login

Thành phần:

- Logo/tên app.
- Email/số điện thoại.
- Password.
- Nút đăng nhập.
- Link đăng ký.

### Screen 2 — Home / Voice Booking

Thành phần:

- Xin chào user.
- Nút micro lớn.
- Text hướng dẫn: “Bấm và nói địa điểm bạn muốn đi.”
- Ví dụ câu nói:
  - “Đặt xe từ VinUni đến Bệnh viện Bạch Mai.”
  - “Đưa tôi về nhà.”

### Screen 3 — Conversation

Thành phần:

- Transcript người dùng nói.
- Phản hồi AI.
- Trạng thái:
  - Đang nghe.
  - Đang xử lý.
  - Cần thêm thông tin.
- Nút micro để trả lời tiếp.

### Screen 4 — Confirmation

Thành phần:

- Điểm đón.
- Điểm đến.
- Loại xe.
- Giá ước tính.
- Nút “Xác nhận đặt xe”.
- Nút “Sửa thông tin”.
- Nút “Hủy”.

### Screen 5 — Booking Status

Thành phần:

- Trạng thái booking:
  - Đã tạo chuyến.
  - Đang tìm tài xế.
  - Đã có tài xế mô phỏng.
- Thông tin chuyến.
- Nút quay về trang chủ.

### Screen 6 — Admin Dashboard

Thành phần:

- Danh sách users.
- Danh sách bookings.
- Conversation logs.
- Extracted intent JSON.

## 11.2. UI Flow chính

```text
Login
  ↓
Home / Voice Button
  ↓
User speaks
  ↓
STT Transcript
  ↓
AI checks missing info
  ├── Missing info → Ask follow-up → User speaks again
  └── Enough info → Confirmation screen
                         ↓
                    User confirms
                         ↓
                   Booking created
                         ↓
                  Booking status
```

## 11.3. Flow thiếu thông tin

```text
User: “Đặt xe đến Bệnh viện Bạch Mai”
AI: “Bạn muốn được đón ở đâu?”
User: “VinUni”
AI: “Bạn muốn đi xe máy hay ô tô?”
User: “Ô tô”
AI: đọc lại thông tin chuyến đi
User: “Xác nhận”
System: tạo booking mock
```

## 11.4. Flow sửa thông tin

```text
User: “Đặt xe từ VinUni đến Bệnh viện Bạch Mai bằng ô tô”
AI: đọc lại thông tin chuyến đi
User: “Không, đổi điểm đến sang Bệnh viện Việt Đức”
AI: cập nhật điểm đến và đọc lại thông tin mới
User: “Xác nhận”
System: tạo booking mock
```

## 11.5. Flow hủy

```text
User: “Đặt xe từ VinUni đến Bệnh viện Bạch Mai”
AI: hỏi loại xe
User: “Tôi không đặt nữa”
AI: “Yêu cầu đặt xe đã được hủy.”
System: không tạo booking
```

---

# 12. GitHub Repo Setup

## 12.1. Tên repo gợi ý

```text
ai20k-244-v-voiceride
```

hoặc

```text
v-voiceride-ai20k
```

## 12.2. Cấu trúc repo

```text
v-voiceride-ai20k/
├── README.md
├── docs/
│   ├── brief.md
│   ├── project-charter.md
│   ├── prd.md
│   ├── architecture.md
│   ├── api-spec.md
│   ├── user-stories.md
│   ├── evaluation-plan.md
│   ├── survey-plan.md
│   └── meeting-notes.md
├── frontend/
│   ├── README.md
│   └── ...
├── backend/
│   ├── README.md
│   └── ...
├── data/
│   ├── sample_locations.json
│   ├── sample_users.json
│   └── test_cases.csv
├── prompts/
│   ├── intent_extraction_prompt.md
│   └── dialogue_prompt.md
├── tests/
│   ├── ai_test_cases.csv
│   └── evaluation_results.csv
├── assets/
│   ├── wireframe-link.md
│   └── screenshots/
├── .gitignore
├── .env.example
└── docker-compose.yml
```

## 12.3. README tối thiểu

```markdown
# V-VoiceRide — AI Voice Booking Assistant

## Overview

V-VoiceRide is a Vietnamese voice-based ride booking assistant for users who have difficulty using traditional ride-hailing apps. The MVP supports voice input, intent extraction, multi-turn clarification, trip confirmation, mock booking, and an admin dashboard for reviewing bookings and conversation logs.

## MVP Features

- User registration and login.
- User/admin role.
- Voice input for ride booking.
- Speech-to-text transcript.
- AI intent extraction.
- Multi-turn clarification.
- Text-to-speech response.
- Confirmation before booking.
- Mock booking service.
- Booking status screen.
- Admin dashboard.
- Conversation logs.
- Online deployment.

## Tech Stack

- Frontend: React / Next.js
- Backend: FastAPI
- Database: PostgreSQL / Supabase
- AI: LLM for intent extraction and dialogue
- Speech: STT/TTS provider
- Deployment: Vercel + Render/Railway/Supabase

## Main Demo Flow

1. User logs in.
2. User taps the microphone button.
3. User says: “Đặt xe từ VinUni đến Bệnh viện Bạch Mai.”
4. AI asks for missing vehicle type if needed.
5. AI reads back the trip information.
6. User confirms.
7. System creates a mock booking.
8. Admin reviews booking and conversation logs.
```

## 12.4. Git commands

```bash
mkdir v-voiceride-ai20k
cd v-voiceride-ai20k

git init

mkdir docs frontend backend data prompts tests assets

touch README.md
touch docs/brief.md
touch docs/project-charter.md
touch docs/prd.md
touch docs/user-stories.md
touch docs/api-spec.md
touch docs/evaluation-plan.md
touch docs/survey-plan.md
touch docs/architecture.md
touch docs/meeting-notes.md

touch .gitignore
touch .env.example

git add .
git commit -m "init project structure and docs"
git branch -M main
git remote add origin https://github.com/<your-username>/v-voiceride-ai20k.git
git push -u origin main
```

PowerShell nếu không có `touch`:

```powershell
New-Item README.md
New-Item docs/brief.md
New-Item docs/project-charter.md
New-Item docs/prd.md
New-Item docs/user-stories.md
New-Item docs/api-spec.md
New-Item docs/evaluation-plan.md
New-Item docs/survey-plan.md
New-Item docs/architecture.md
New-Item docs/meeting-notes.md
New-Item .gitignore
New-Item .env.example
```

## 12.5. GitHub Issues nên tạo ngay

```text
[DOCS] Write 1-page brief
[DOCS] Write PRD v1
[DOCS] Define user stories
[DESIGN] Create user flow diagram
[DESIGN] Create low-fi wireframe
[SETUP] Initialize frontend project
[SETUP] Initialize backend project
[SETUP] Create database schema draft
[AI] Define intent extraction schema
[AI] Create initial prompt for booking intent
[AI] Create 30 Vietnamese voice command test cases
[QA] Create evaluation plan
[PM] Create sprint board and milestones
```

---

# 13. Survey riêng nhóm nên làm

## 13.1. Vì sao vẫn cần khảo sát riêng?

Các nguồn công khai giúp chứng minh đề tài có cơ sở. Tuy nhiên, để chốt MVP, nhóm cần biết người dùng trong bối cảnh Việt Nam thực sự gặp khó ở đâu và có muốn dùng voice không.

## 13.2. Google Form nên hỏi

1. Bạn đã từng dùng app đặt xe công nghệ chưa?
   - Có
   - Không

2. Bạn có từng đặt xe hộ người thân không?
   - Có
   - Không

3. Người bạn từng đặt hộ là ai?
   - Bố/mẹ
   - Ông/bà
   - Người thân lớn tuổi
   - Bạn bè
   - Khác

4. Theo bạn, bước nào khó nhất khi đặt xe?
   - Nhập điểm đón
   - Nhập điểm đến
   - Chọn đúng địa điểm gợi ý
   - Chọn loại xe
   - Đọc giá
   - Xác nhận chuyến
   - Theo dõi tài xế
   - Thanh toán

5. Bạn hoặc người thân có từng nhập sai điểm đón/điểm đến không?
   - Có
   - Không
   - Không nhớ

6. Bạn có muốn dùng giọng nói để đặt xe không?
   - Thang 1–5

7. Bạn lo ngại điều gì nhất nếu AI hỗ trợ đặt xe?
   - AI nghe sai
   - AI đặt sai điểm đến
   - AI đặt nhầm loại xe
   - Không biết giá
   - Không biết tài xế ở đâu
   - Không tin AI
   - Khác

8. Trước khi đặt, bạn muốn hệ thống đọc lại thông tin nào?
   - Điểm đón
   - Điểm đến
   - Loại xe
   - Giá ước tính
   - Thời gian tài xế đến
   - Biển số xe

9. Bạn muốn xác nhận bằng cách nào?
   - Nói “Xác nhận”
   - Bấm nút xác nhận lớn
   - Cả hai
   - Người thân xác nhận hộ

10. Nếu có một app đặt xe bằng giọng nói tiếng Việt, bạn muốn tính năng nào nhất?

## 13.3. Phỏng vấn 5–8 người

Nên phỏng vấn:

- 2–3 người lớn tuổi.
- 1–2 người ít dùng app.
- 1–2 người từng đặt xe hộ bố mẹ/ông bà.
- Nếu có thể, 1 người khiếm thị hoặc dùng screen reader.

Câu hỏi:

1. Lần gần nhất cô/chú/anh/chị đặt xe là khi nào?
2. Bước nào khó nhất?
3. Có từng nhờ người khác đặt hộ không?
4. Có từng nhập sai địa chỉ không?
5. Có sợ bấm nhầm không?
6. Nếu dùng giọng nói, muốn nói như thế nào?
7. Trước khi đặt, hệ thống cần đọc lại thông tin gì?
8. Có tin AI đặt xe hộ không?
9. Nếu AI nghe sai, muốn sửa bằng cách nào?
10. Một bản demo như thế nào thì thấy hữu ích?

---

# 14. Evaluation Plan

## 14.1. Functional Test

Kiểm tra:

- Đăng ký.
- Đăng nhập.
- Phân quyền.
- Gửi message text.
- Gửi voice.
- Tạo booking.
- Xem booking.
- Admin xem log.

## 14.2. AI Workflow Test

Kiểm tra:

- Trích xuất pickup.
- Trích xuất dropoff.
- Trích xuất vehicle_type.
- Hỏi lại khi thiếu thông tin.
- Sửa thông tin.
- Hủy session.
- Không tạo booking khi chưa xác nhận.

## 14.3. User Testing

Kiểm tra:

- Người dùng có hiểu cách dùng không.
- Người dùng có hoàn thành booking không.
- Người dùng thấy dễ dùng không.
- Người dùng có tin hệ thống không.
- Người dùng có thấy voice hữu ích không.

## 14.4. Metrics

| Metric | Target |
|---|---:|
| Hoàn thành booking mock trong test case chuẩn | ≥ 80% |
| Trích xuất đúng pickup | ≥ 80% |
| Trích xuất đúng dropoff | ≥ 80% |
| Trích xuất đúng vehicle_type | ≥ 80% |
| Hỏi lại đúng khi thiếu thông tin | ≥ 90% |
| Booking có xác nhận cuối | 100% |
| Không tạo booking khi thiếu thông tin quan trọng | 100% |
| User testing | ≥ 5 người |
| Test cases | 30–50 |

## 14.5. Test case mẫu

| ID | Input | Expected Output |
|---|---|---|
| TC01 | Đặt xe từ VinUni đến Bệnh viện Bạch Mai | Hỏi loại xe nếu thiếu |
| TC02 | Đặt ô tô từ VinUni đến Bệnh viện Bạch Mai | Đọc lại và yêu cầu xác nhận |
| TC03 | Tôi muốn đi bệnh viện | Hỏi điểm đón và bệnh viện nào |
| TC04 | Đưa tôi về nhà | Lấy saved place Nhà nếu có |
| TC05 | Đổi điểm đến sang Việt Đức | Cập nhật dropoff |
| TC06 | Tôi muốn đi xe máy | Cập nhật vehicle_type |
| TC07 | Hủy chuyến | Hủy session, không tạo booking |
| TC08 | Xác nhận | Tạo booking nếu đủ thông tin |
| TC09 | Không đúng | Quay lại bước sửa thông tin |
| TC10 | Đặt xe đi chơi | Hỏi lại điểm đến cụ thể |

---

# 15. Risk & Mitigation

| Risk | Tác động | Mitigation |
|---|---|---|
| STT nghe sai tiếng Việt | AI hiểu sai yêu cầu | Hiển thị transcript, đọc lại thông tin, yêu cầu xác nhận |
| LLM trả sai JSON | Backend lỗi | Validate schema, retry, fallback |
| Người dùng nói thiếu thông tin | Không đặt được xe | AI hỏi lại từng field |
| Địa điểm mơ hồ | Đặt sai điểm | Hỏi lại hoặc yêu cầu nói rõ hơn |
| Người dùng không tin AI | Không dám dùng | Luôn có confirmation cuối bằng text + voice |
| Scope quá rộng | Không kịp 6 tuần | Chỉ làm booking mock |
| Deploy lỗi | Không demo được | Có video backup và local fallback |
| UI khó dùng | Người lớn tuổi khó thao tác | Simple Mode, nút lớn, chữ lớn |
| Thành viên đều tập trung AI, thiếu tích hợp | Chậm end-to-end | Chia task theo module, tuần 2 phải có text booking end-to-end |

---

# 16. Checklist hoàn thành Sprint 0 / Tuần 1

## 16.1. Brief

- [ ] Có problem statement.
- [ ] Có target users.
- [ ] Có proposed solution.
- [ ] Có MVP scope.
- [ ] Có out-of-scope.
- [ ] Có success metrics.

## 16.2. PRD

- [ ] Có overview.
- [ ] Có goals/non-goals.
- [ ] Có main user flow.
- [ ] Có functional requirements.
- [ ] Có AI workflow.
- [ ] Có metrics.
- [ ] Có risks.
- [ ] Có milestones.

## 16.3. Wireframe/UI Flow

- [ ] Có Login screen.
- [ ] Có Home/Voice Button screen.
- [ ] Có Conversation screen.
- [ ] Có Confirmation screen.
- [ ] Có Booking Status screen.
- [ ] Có Admin Dashboard.
- [ ] Có flow thiếu thông tin.
- [ ] Có flow sửa thông tin.
- [ ] Có flow hủy.

## 16.4. GitHub Repo

- [ ] Có repo.
- [ ] Có README.
- [ ] Có `docs/`.
- [ ] Có `frontend/`.
- [ ] Có `backend/`.
- [ ] Có `prompts/`.
- [ ] Có `tests/`.
- [ ] Có `.env.example`.
- [ ] Có `.gitignore`.
- [ ] Có GitHub Issues.
- [ ] Có Project Board.

## 16.5. AI Preparation

- [ ] Có intent schema v1.
- [ ] Có prompt extraction v1.
- [ ] Có dialogue states v1.
- [ ] Có 30 câu lệnh test ban đầu.
- [ ] Có plan đánh giá STT.

## 16.6. Validation

- [ ] Có Google Form khảo sát.
- [ ] Có kế hoạch phỏng vấn 5–8 người.
- [ ] Có danh sách câu hỏi phỏng vấn.
- [ ] Có bảng tổng hợp secondary research.

---

# 17. Tài liệu tham khảo

## [S1] Rakuten Insight — 2025 Ride-Hailing App Landscape in Vietnam

URL: https://insight.rakuten.com/2025-ride-hailing-app-landscape-in-vietnam/

Dùng để chứng minh bối cảnh ride-hailing tại Việt Nam và các thương hiệu phổ biến.

## [S2] Grab Product Team — Grab’s AI Voice Assistant lets visually impaired users book rides with ease

URL: https://www.grab.com/sg/inside-grab/stories/grabs-ai-voice-assistant-lets-visually-impaired-users-book-rides-with-ease/

Dùng làm case study gần nhất với đề tài voice booking assistant.

## [S3] Frontier Enterprise — Grab powers on AI Centre of Excellence

URL: https://www.frontier-enterprise.com/grab-powers-on-ai-center-of-excellence/

Dùng cho thông tin Grab fine-tune STT với local voice samples và cải thiện recognition.

## [S4] Mineta Transportation Institute — Will Ride-Hailing Enhance Mobility for Older Adults? A California Survey

URL: https://transweb.sjsu.edu/mctm/research/utc/Will-Ride-Hailing-Enhance-Mobility-Older-Adults-California-Survey

Dùng để chứng minh người lớn tuổi là nhóm phù hợp để nghiên cứu ride-hailing accessibility.

## [S5] ROSA P / U.S. DOT — Will Ride-Hailing Enhance Mobility for Older Adults? A California Survey

URL: https://rosap.ntl.bts.gov/view/dot/53557

Nguồn bổ sung cho nghiên cứu khảo sát 2.917 người từ 55 tuổi trở lên.

## [S6] Misra et al. — How Older Adults Use Ride-hailing Booking Technology in California

URL: https://www.shirgaokar.com/uploads/1/6/1/2/16129606/misra_et_al._-_2021_-_how_older_adults_use_ride-hailing_booking_technology_in_california.pdf

Dùng cho insight về cách người lớn tuổi tự đặt xe hoặc nhờ người khác đặt.

## [S7] AARP — Tech Use and Adoption Keeps Surging Among Older Adults

URL: https://www.aarp.org/pri/topics/technology/internet-media-devices/2026-technology-trends-older-adults/

Dùng để chứng minh người trên 50 tuổi dùng công nghệ ngày càng nhiều nhưng vẫn cần thiết kế phù hợp.

## [S8] Axios — Uber launches senior accounts to simplify rides for older adults

URL: https://www.axios.com/2025/06/04/uber-app-senior-account-simple-mode

Dùng để tham khảo Simple Mode, senior accounts, family profile/caregiver support.

## [S9] The Verge — Uber senior accounts with larger typeface and fewer buttons

URL: https://www.theverge.com/news/678874/uber-senior-account-elderly-font-simple

Dùng để tham khảo UI accessibility: font lớn, ít nút, simplified navigation, saved destinations.

---

# 18. Kết luận ngắn

V-VoiceRide nên được triển khai như một **workflow AI có kiểm soát**, không phải Agent tự chủ. Core value của MVP là giúp người dùng khó thao tác app có thể hoàn thành quy trình đặt xe mô phỏng bằng giọng nói tiếng Việt, với các guardrail quan trọng: hỏi lại khi thiếu thông tin, hiển thị transcript, đọc lại chuyến đi và bắt buộc xác nhận trước booking.

Trong Sprint 0/Tuần 1, nhóm cần hoàn thành 4 deliverables chính:

1. **Brief** — chốt problem, user, scope, metric.
2. **PRD** — chốt requirements, AI workflow, risks, milestones.
3. **Wireframe/UI Flow** — chốt trải nghiệm user/admin.
4. **GitHub Repo Setup** — tạo nền để code và quản lý task.

Nếu 4 deliverables này rõ, từ tuần 2 nhóm có thể bắt đầu làm text booking end-to-end, sau đó thêm voice ở tuần 3 và tiến tới deploy/evaluation ở tuần 5.
