# V-VoiceRide

**V-VoiceRide** là MVP trong giai đoạn AI20K Build Phase cho bài toán **trợ lý đặt xe bằng giọng nói tiếng Việt**. Sản phẩm không phải ứng dụng gọi xe thật như Grab/Be/Xanh SM, mà là một hệ thống mô phỏng an toàn để chứng minh người dùng có thể hoàn thành quy trình đặt xe thông qua hội thoại giọng nói, xác nhận rõ ràng và trạng thái booking mock.

## Bài Toán

Ứng dụng gọi xe đã phổ biến tại Việt Nam, nhưng một số nhóm người dùng như người lớn tuổi, người khiếm thị hoặc người ít tự tin với công nghệ vẫn có thể gặp khó khăn khi thao tác nhiều bước trên app. V-VoiceRide thu hẹp bài toán vào một nhiệm vụ cụ thể: giúp người dùng đặt một chuyến xe mô phỏng bằng cách nói tự nhiên bằng tiếng Việt.

## Phạm Vi MVP

- Web app thân thiện với mobile.
- Đăng nhập với vai trò user và admin.
- Luồng đặt xe bằng giọng nói, có hiển thị transcript.
- STT để chuyển giọng nói thành văn bản, LLM để trích xuất intent, TTS để phản hồi bằng giọng nói.
- Hội thoại nhiều lượt khi thiếu điểm đón, điểm đến hoặc loại xe.
- Bắt buộc xác nhận cuối trước khi tạo booking mock.
- Trạng thái booking mock và admin dashboard để xem booking/conversation logs.

Ngoài phạm vi MVP: điều phối tài xế thật, thanh toán thật, bản đồ/routing production, tích hợp trực tiếp với Grab/Be/Xanh SM.

## Tech Stack

| Layer | Công nghệ |
|---|---|
| Backend | FastAPI, Pydantic |
| Agent | LangGraph, LangChain, OpenAI |
| Voice | Browser Web Speech API cho prototype, sau đó có thể dùng STT/TTS tương thích OpenAI |
| Database | SQLite cho development, sẵn sàng chuyển PostgreSQL |
| Testing | pytest, pytest-asyncio, httpx, ruff |
| DevOps | Docker, GitHub Actions |

## Chạy Project

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -e ".[dev]"
copy .env.example .env
uvicorn src.main:app --reload --port 8000
```

Mở API docs tại `http://localhost:8000/docs`.

## Tài Liệu Sprint 0

- [1-page brief](docs/brief.md)
- [PRD](docs/prd.md)
- [Wireframe / UI flow](docs/wireframe.md)
- [GitHub repo setup](docs/github-setup.md)

File tổng hợp đầy đủ của dự án được giữ tại [AI20K244_VoiceRide_Project_Package.md](AI20K244_VoiceRide_Project_Package.md).

## Trạng Thái Repo

Repo này đã được chuyển từ AI20K starter template sang baseline cho V-VoiceRide. Tài liệu hướng dẫn của template vẫn được giữ trong `docs/guide/` để tham khảo, còn tài liệu sản phẩm đang dùng nằm trực tiếp trong `docs/`.
