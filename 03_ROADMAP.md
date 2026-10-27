# 5 giai đoạn Codex

## GĐ0 — Khởi tạo và nền tảng
- scaffold Python/PySide6/FastAPI, `run.ps1`, `.env.example`, dependencies khóa version, gitignore, ruff/pytest.
- DB schema, Alembic migrations, DPAPI adapter, structured logs có scrub secrets, health checks.
- Mock Meta client và seed 500 Page, ~2000 job/ngày.
- Nghiệm thu: cài và chạy Windows PC offline, tests pass, seed/restore thành công.

## GĐ1 — Quản lý Page & lịch nội dung
- dashboard, CRUD/tag/group/sort/filter Pages, Content Library/Composer, job queue và Calendar.
- human approval, duplicate warnings, deterministic per-page content, bulk schedule preview.
- Nghiệm thu: 500 Page mock, lịch không mất sau restart; UI không bị đơ khi lọc.

## GĐ2 — Meta kết nối thật & xuất bản
- OAuth + permissions, `/me/accounts`, Page token encrypted.
- publish text/photo/album/link, Reels multistep upload với progress, processing, finish, remote verification.
- rate adaptive, retry/reconcile, error classification, permission diagnostics.
- Nghiệm thu: 1–3 Page do mình quản lý, đăng bài thật có post URL, retry không sinh trùng.

## GĐ3 — Bình luận/Insights/Browser/AI
- bình luận người thật, reply/moderate với phê duyệt; alerts.
- Insights registry API v26+, trend; export, so sánh Page; mock fallback cho metrics deprecated.
- Browser manual launcher + optional proxy config + test; template AI offline, AI provider optional OFF.
- Nghiệm thu: dashboard đủ cập nhật với 10 Page live; metrics null khi unsupported.

## GĐ4 — 500 Page scale & đóng gói
- load test 2000–5000 jobs, retry storms, Windows sleep/restart, quota budgets.
- storage retention, backup rotation, restore drill, performance & packaging PyInstaller.
- Nghiệm thu: chạy 72h MOCK không mất job; chạy LIVE tăng dần theo quyền/limit Meta; minh bạch chỗ chưa test.

Không mặc định tất cả 500 Page đều dùng được API. Khả năng thực tế phụ thuộc Page ownership, granted permissions, App Review, limit Meta, chất lượng mạng.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
