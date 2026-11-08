# Scopus-Ictu-BE

Backend (FastAPI + PostgreSQL + SQLAlchemy/Alembic) của hệ thống quản lý và chuẩn hóa hồ sơ tác giả, công bố khoa học
Scopus cho ICTU. Giao diện web ở repo [Scopus-Ictu-FE](https://github.com/qhun22/Scopus-Ictu-FE).

> Repo này được đồng bộ từ repo chính [Scopus-Ictu](https://github.com/qhun22/Scopus-Ictu) (commit `753547d`). Mọi thay đổi mã nguồn làm ở repo chính.

## Cấu trúc

- `backend/` — mã nguồn API (`app/`), migration (`alembic/`), script tiện ích (`scripts/`), kiểm thử (`tests/`).
- `data/` — chỉ có lược đồ (schema) và thư mục rỗng; dữ liệu thật không bao giờ được đưa lên.
- `scopus-ictu-qhun22.bat` — trình khởi động máy thử nghiệm (gọi `backend/scripts/demo_launcher.py`); có kiểm thử đi kèm.

## Chạy

```bash
cd backend
cp .env.example .env          # điền DB_*, SECRET_KEY, ENVIRONMENT, BACKEND_CORS_ORIGINS
python -m pip install -e ".[dev]"
python -m alembic upgrade head
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Kiểm thử cần `TEST_DATABASE_URL` trỏ tới một CSDL kiểm thử riêng (`tests/db_safety_guard.py`):

```bash
cd backend
python -m pytest -q
```
