# 🦾 GoClaw — AI Agent Gateway

> **Tài liệu tham chiếu chính thức cho máy này.**  
> Không sửa trực tiếp — hỏi Antigravity để cập nhật.  
> Cài tại: `C:\goclaw` | Binary: `C:\goclaw\goclaw.exe`

---

## 📌 Tóm tắt

| Thông tin | Chi tiết |
|-----------|----------|
| **Phần mềm** | GoClaw — Multi-Tenant AI Agent Gateway |
| **Mục đích** | Chạy và quản lý nhiều AI agent, kết nối 20+ LLM provider |
| **Ngôn ngữ core** | Go 1.26 |
| **Web UI** | React 19 + Vite 6 + TypeScript + Tailwind CSS 4 |
| **Database** | PostgreSQL 18 (server) / SQLite (desktop/lite) |
| **Trạng thái** | ✅ Đã cài tại `C:\goclaw` (binary: `goclaw.exe` ~42 MB) |
| **Phiên bản** | Xem `CHANGELOG.md` tại `C:\goclaw\CHANGELOG.md` |
| **Docs chính thức** | https://docs.goclaw.sh |
| **Source gốc** | https://github.com/nextlevelbuilder/goclaw |

---

## 🗂️ Cấu trúc thư mục tại `C:\goclaw`

```
C:\goclaw\
├── goclaw.exe           ← Binary chính (~42 MB), chạy trực tiếp
├── .env.example         ← Template biến môi trường (copy thành .env)
├── docker-compose.yml   ← Chạy qua Docker (có PostgreSQL)
├── CLAUDE.md            ← Tài liệu kỹ thuật nội bộ (cho AI đọc)
├── CHANGELOG.md         ← Lịch sử thay đổi
├── cmd/                 ← CLI commands
├── internal/            ← Logic backend
├── ui/web/              ← Web dashboard (React)
├── ui/desktop/          ← Desktop app (Wails)
├── migrations/          ← Database migrations
└── skills/              ← Skill definitions
```

---

## ⚡ Cách khởi động

### Cách 1 — Desktop Lite (Đơn giản nhất, dùng SQLite)

```powershell
# Chạy trực tiếp binary (không cần Docker, không cần PostgreSQL)
C:\goclaw\goclaw.exe
```

Sau đó mở trình duyệt: **http://localhost:18790**

### Cách 2 — Server Mode với Docker (Đầy đủ tính năng)

```powershell
cd C:\goclaw

# Bước 1: Tạo file .env từ template
Copy-Item .env.example .env
# Rồi điền GOCLAW_GATEWAY_TOKEN, GOCLAW_ENCRYPTION_KEY, POSTGRES_PASSWORD vào .env

# Bước 2: Khởi động (tự migrate DB, tự build)
make up
# Hoặc: docker compose up -d
```

### Cách 3 — Onboard lần đầu (từ source)

```powershell
cd C:\goclaw
.\goclaw.exe onboard    # Wizard thiết lập lần đầu
# Sau đó chạy:
.\goclaw.exe
```

---

## 🔑 Biến môi trường cần thiết (`.env`)

```env
# --- Bắt buộc ---
GOCLAW_GATEWAY_TOKEN=    # Token xác thực gateway (tự sinh)
GOCLAW_ENCRYPTION_KEY=   # Khóa AES-256-GCM (tự sinh)
POSTGRES_PASSWORD=       # Mật khẩu PostgreSQL (nếu dùng Docker)

# --- Không bắt buộc ---
# GOCLAW_POSTGRES_DSN=postgres://user:pass@host:5432/dbname?sslmode=disable
# GOCLAW_TRACE_VERBOSE=1
```

> ⚠️ Secrets KHÔNG được lưu trong `config.json`. Chỉ lưu trong `.env` hoặc biến môi trường hệ thống.

---

## 🧩 Tính năng chính

| Tính năng | Mô tả |
|-----------|-------|
| **20+ LLM Providers** | Anthropic, OpenAI, Gemini, DeepSeek, Groq, Ollama... |
| **7 Kênh nhắn tin** | Telegram, Discord, Slack, Zalo, Feishu, WhatsApp |
| **Agent Teams** | Task board, delegation sync/async giữa các agent |
| **Multi-tenant** | Nhiều user, nhiều team, workspace riêng biệt |
| **Memory** | pgvector semantic search + FTS |
| **MCP** | Model Context Protocol bridge |
| **Cron/Scheduler** | Lập lịch tự động cho agent |
| **Security** | AES-256-GCM, rate limiting, SSRF protection |

---

## 🖥️ Hai phiên bản

| | Desktop Lite | Server (Standard) |
|-|-------------|------------------|
| Database | SQLite (local) | PostgreSQL 18 |
| Cài đặt | Chạy 1 file exe | Docker Compose |
| Agents | Tối đa 5 | Không giới hạn |
| Kênh nhắn tin | Không | Telegram, Discord... |
| Multi-tenant | Không | Có |
| Port | 18790 (localhost) | 18790 |

---

## ❓ GoClaw với Vibe Coding (Nonteck approach) — Nhận xét

| Tình huống | Đánh giá |
|-----------|----------|
| Chạy GoClaw Lite để dùng AI agent | ✅ Rất dễ — chỉ cần mở exe |
| Cấu hình agent qua Web UI | ✅ Không cần code |
| Dùng Antigravity viết skill/config cho GoClaw | ✅ Rất phù hợp |
| Kết nối Telegram bot với GoClaw | ✅ Qua Web Dashboard |
| Tự sửa source code Go | ❌ Không cần thiết với Vibe Coding |

**→ Kết luận:** GoClaw **hoàn toàn phù hợp** với phong cách Vibe Coding / Nonteck. Phần lớn cấu hình qua Web UI tại `http://localhost:18790`. Dùng Antigravity để tạo/sửa skill files khi cần.

---

## 🔄 Lịch sử cập nhật

| Ngày | Nội dung |
|------|----------|
| 2026-04-07 | ✅ Xác nhận đã cài tại `C:\goclaw` (goclaw.exe ~42 MB). Tạo tài liệu lần đầu |

---

*Tài liệu được quản lý bởi Antigravity. Chat để cập nhật.*
