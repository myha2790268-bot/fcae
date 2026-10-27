# Mô hình dữ liệu đề xuất

## Bảng
- `operators(id, display_name, created_at)` — người quản lý hợp lệ.
- `operator_auth(id, operator_id, provider, meta_user_id, token_ref, granted_scopes_json, health, connected_at, checked_at)`.
- `pages(id, meta_page_id UNIQUE, name, operator_id, category, tz, state, connected_at, last_sync_at)`.
- `page_groups(id, name)` và `page_group_links(page_id, group_id UNIQUE)`.
- `browser_profiles(id, operator_id, browser, user_data_dir, proxy_ref, last_opened_at)`.
- `proxy_configs(id, kind, endpoint, username_ref, password_ref, active, created_at)`.
- `assets(id, file_path, sha256 UNIQUE, mime_type, bytes, duration_sec, width, height, license_note, created_at)`.
- `content_templates(id, title, body, format, status, created_at)`, `content_versions(id, template_id, version, caption, media_refs_json, approved_at)`.
- `campaigns(id, name, status, created_at)`, `publish_slots(id, campaign_id, page_id, content_version_id, scheduled_at_utc, approval_state)`.
- `jobs(id UUID PK, slot_id UNIQUE, page_id, job_type, state, attempt_count, lease_until, next_retry_at, remote_id, last_error_code, created_at, updated_at)`.
- `job_events(id, job_id, from_state, to_state, message_redacted, created_at)`.
- `reel_uploads(id, job_id UNIQUE, remote_video_id, upload_session_ref, uploaded_bytes, processing_status, verified_at)`.
- `comments(id, page_id, object_id, remote_comment_id UNIQUE, message, author_public_id_nullable, created_at, moderation_state)`.
- `comment_replies(id, comment_id, draft_text, approval_state, remote_reply_id, sent_at)`.
- `metric_definitions(id, source, metric_name UNIQUE, definition, supported, replaced_by, api_min_version)`.
- `metric_snapshots(id, page_id, object_id_nullable, metric_name, metric_date, observed_at, value_nullable, source_version)`.
- `notifications(id, severity, category, object_id, message, read_at, created_at)`.
- `settings(key PRIMARY KEY, value_json)` và `audit_log(id, actor, action, target, redacted_detail, created_at)`.

## Quy tắc không thay đổi
- UNIQUE(meta_page_id), UNIQUE(slot_id jobs), UNIQUE(job.remote_id khi not null nếu phù hợp).
- Con trỏ remote video luôn lưu ngay sau create session; không upload lại mà không kiểm tra trạng thái.
- Job update bằng transaction + lease; `published` chỉ khi xác minh remote hoặc response chứng minh xuất bản thành công.
- Không dùng TEXT plaintext lưu Facebook access token, app secret, proxy password.
- Tất cả thời gian lưu UTC; UI quy đổi Asia/Ho_Chi_Minh hoặc múi giờ Page.
- Metric thất bại/không được quyền phải là NULL cùng reason; không chuyển NULL thành 0.


> **Phần cập nhật bắt buộc:** đọc thêm `09_PROJECT_MANAGER.md`, `10_BULK_PUBLISHER_UI.md`, `11_OFFLINE_CLOUD_SCHEDULING.md`, `12_UI_UX_SPEC.md`, `13_API_CONTRACTS.md`, `14_SECURITY_POLICY.md` và `15_ACCEPTANCE_CHECKLIST.md`. Nếu có khác biệt, các tài liệu 09–15 và AGENTS.md được ưu tiên.
