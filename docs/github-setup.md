# V-VoiceRide GitHub Repo Setup

## Repository Hiện Tại

- Local repo: `C:\study\lab_aiinaction\C2-App-161`
- Remote: `https://github.com/BNK2610/C2-App-161.git`
- Branch làm việc mặc định nên là `main`.
- Tài liệu sản phẩm đang dùng nằm trong `docs/`.
- Tài liệu hướng dẫn của template được giữ trong `docs/guide/` để tham khảo.

## Quy Trình Branch Đề Xuất

```text
main
|-- develop
    |-- feature/voice-booking-flow
    |-- feature/intent-extraction
    |-- feature/mock-booking-admin
    |-- docs/sprint-0-deliverables
```

## Checklist Repo

- [x] README đã mô tả V-VoiceRide thay vì starter template.
- [x] Metadata trong `pyproject.toml` đã đổi package thành `voiceride`.
- [x] `.env.example` đã căn chỉnh theo cấu hình MVP của VoiceRide.
- [x] Đã tạo tài liệu Sprint 0:
  - `docs/brief.md`
  - `docs/prd.md`
  - `docs/wireframe.md`
  - `docs/github-setup.md`
- [x] CI workflow đã có tại `.github/workflows/ci.yml`.
- [ ] Tạo GitHub issues cho các epic của MVP.
- [ ] Bật bảo vệ branch `main` sau khi có bản push ổn định đầu tiên.
- [ ] Tạo project board với các cột: Backlog, Ready, In Progress, Review, Done.
- [ ] Bổ sung deployment URL sau khi deploy backend/frontend.

## GitHub Issues Đề Xuất

1. Chốt data model và API contract cho VoiceRide.
2. Implement endpoint đặt xe bằng voice/text.
3. Implement prompt trích xuất intent và validation.
4. Implement state machine cho bước hỏi lại và xác nhận.
5. Implement lưu booking mock.
6. Xây dựng UI đặt xe trên mobile web.
7. Xây dựng admin dashboard và màn hình conversation log.
8. Thêm kịch bản evaluation và test report.
9. Deploy backend và frontend.
10. Quay video demo và cập nhật presentation.

## Setup Môi Trường

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -e ".[dev]"
copy .env.example .env
pytest
```

## Kỳ Vọng CI

CI nên cài dependencies, chạy `ruff check src/ tests/` và chạy `pytest tests/`. Ở giai đoạn demo week, nhóm có thể bổ sung deployment check sau khi có live URL.
