# threetl

Dự án Python được quản lý và phát triển bằng [**uv**](https://docs.astral.sh/uv/) — công cụ quản lý package và môi trường Python siêu nhanh (viết bằng Rust).

---

## 🚀 1. Cài đặt `uv`

Nếu máy bạn chưa có `uv`, hãy cài đặt bằng lệnh tương ứng với hệ điều hành:

### Linux / macOS
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Windows (PowerShell)
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### Cài qua `pip` hoặc `brew` (Tùy chọn)
```bash
# Qua Homebrew (macOS/Linux)
brew install uv

# Hoặc qua pip
pip install uv
```

Kiểm tra cài đặt thành công:
```bash
uv --version
```

---

## 🛠️ 2. Các lệnh cơ bản với dự án

### 2.1. Cài đặt môi trường & dependencies
Để tự động tạo môi trường ảo `.venv` và đồng bộ mọi dependencies từ `pyproject.toml`:
```bash
uv sync
```

### 2.2. Chạy ứng dụng
Với `uv`, bạn **không cần kích hoạt môi trường ảo thủ công**, `uv run` sẽ tự động kích hoạt venv và thực thi:
```bash
# Chạy script đã cấu hình trong pyproject.toml
uv run threetl

# Hoặc chạy trực tiếp file code
uv run python src/threetl/__init__.py
```

### 2.3. (Tùy chọn) Kích hoạt môi trường ảo thủ công
Nếu bạn muốn dùng terminal như môi trường thông thường:
* **Linux / macOS:**
  ```bash
  source .venv/bin/activate
  ```
* **Windows:**
  ```powershell
  .venv\Scripts\activate
  ```

---

## 📦 3. Quản lý thư viện (Dependencies)

### 3.1. Cài thêm thư viện mới
Lệnh này sẽ tự động tải thư viện, ghi vào `pyproject.toml` và cập nhật file khóa `uv.lock`:
```bash
# Cài một thư viện (ví dụ: requests)
uv add requests

# Cài nhiều thư viện cùng lúc
uv add fastapi uvicorn pydantic
```

### 3.2. Cài thư viện cho môi trường phát triển (Dev dependencies)
Dành cho các công cụ như linter, test, formatter:
```bash
uv add --dev pytest ruff
```

### 3.3. Gỡ bỏ thư viện
```bash
uv remove requests
```

### 3.4. Nâng cấp các thư viện
```bash
# Cập nhật toàn bộ dependencies lên bản mới nhất phù hợp
uv lock --upgrade
uv sync
```

---

## 🐍 4. Quản lý phiên bản Python

Dự án hiện đang cấu hình dùng **Python 3.13** (xem tại file `.python-version` và `pyproject.toml`).

* **Tự động tải và cài phiên bản Python yêu cầu:**
  ```bash
  uv python install 3.13
  ```
* **Xem danh sách các phiên bản Python có trên máy:**
  ```bash
  uv python list
  ```
* **Đổi phiên bản Python cho dự án:**
  ```bash
  uv python pin 3.12
  ```

---

## ⚡ 5. Tiện ích chạy nhanh (`uvx`)

`uvx` cho phép bạn chạy ngay một công cụ Python CLI mà không cần phải cài đặt nó vào dự án:
```bash
# Kiểm tra code bằng linter ruff
uvx ruff check .

# Format code tự động
uvx ruff format .
```

---

## 📂 Cấu trúc thư mục

```text
THREETL/
├── .agents/skills/      # Thư mục chứa các AI Agent Skills
├── .python-version      # Định nghĩa phiên bản Python dùng cho dự án (3.13)
├── pyproject.toml       # Cấu hình dự án, metadata, dependencies và build-system
├── skills-lock.json     # Quản lý phiên bản & nguồn tải của các skills
├── uv.lock              # File khóa phiên bản chính xác của các thư viện
├── README.md            # Tài liệu hướng dẫn sử dụng
└── src/
    └── threetl/
        └── __init__.py  # Mã nguồn chính của dự án
```

---

## 🤖 6. Danh sách AI Agent Skills trong dự án

Dự án hiện đang tích hợp **14 skills** tại `.agents/skills/`, giúp các trợ lý AI (Antigravity, Cursor, Claude Code...) tạo mã nguồn chất lượng cao, thiết kế giao diện có gu thẩm mỹ (anti-slop) và tuân thủ các nguyên tắc UX/UI hiện đại:

### 🎨 6.1. Thiết kế & Thẩm mỹ Frontend (UI/UX Taste)
| Skill | Mô tả chức năng |
| :--- | :--- |
| [`design-taste-frontend`](.agents/skills/design-taste-frontend/SKILL.md) | **(Mặc định v2)** Bộ khung chống "AI slop", tự động phân tích brief để chọn phong cách (minimalist, editorial, SaaS...), tối ưu typography và spacing. |
| [`design-taste-frontend-v1`](.agents/skills/design-taste-frontend-v1/SKILL.md) | Phiên bản Taste-Skill v1 ban đầu (dùng khi cần độ tương thích ngược). |
| [`high-end-visual-design`](.agents/skills/high-end-visual-design/SKILL.md) | Định hình phong cách chuẩn Agency cao cấp: chọn font, hiệu ứng shadow phân tầng, cấu trúc card và micro-animation. |
| [`minimalist-ui`](.agents/skills/minimalist-ui/SKILL.md) | Thiết kế giao diện phong cách editorial tối giản, monochrome ấm áp, typography tương phản, flat bento grid không bóng đổ gắt. |
| [`industrial-brutalist-ui`](.agents/skills/industrial-brutalist-ui/SKILL.md) | Giao diện cơ khí công nghiệp (Swiss typography kết hợp terminal quân sự), phù hợp với dashboard dữ liệu và blueprint. |
| [`gpt-taste`](.agents/skills/gpt-taste/SKILL.md) | Kỹ sư UX/UI & GSAP Motion: phân bố cấu trúc AIDA, gapless bento, typography dạng rộng và hiệu ứng GSAP ScrollTrigger. |
| [`stitch-design-taste`](.agents/skills/stitch-design-taste/SKILL.md) | Tạo file `DESIGN.md` chuẩn ngữ nghĩa cho Google Stitch để quản lý design system đồng nhất. |

### 🔍 6.2. Kiểm định & Cải tiến giao diện (Audit & Redesign)
| Skill | Mô tả chức năng |
| :--- | :--- |
| [`apple-design`](.agents/skills/apple-design/SKILL.md) | Review và audit UI/UX theo tiêu chuẩn **Apple Human Interface Guidelines (HIG)**, hiệu ứng Liquid Glass, dark mode, thiết kế cho iOS/macOS/Flutter/React Native. |
| [`redesign-existing-projects`](.agents/skills/redesign-existing-projects/SKILL.md) | Nâng cấp giao diện có sẵn, quét tìm và loại bỏ các pattern generic AI, cải thiện thẩm mỹ mà không phá vỡ logic cũ. |

### 🖼️ 6.3. Tạo hình ảnh & Visual Assets
| Skill | Mô tả chức năng |
| :--- | :--- |
| [`image-to-code`](.agents/skills/image-to-code/SKILL.md) | Quy trình Image-to-Code: Yêu cầu AI tạo ảnh mockup chi tiết trước, phân tích kỹ rồi sinh code tái hiện chuẩn xác. |
| [`imagegen-frontend-web`](.agents/skills/imagegen-frontend-web/SKILL.md) | Sinh ảnh reference cho từng section riêng biệt của website/landing page, đảm bảo phong cách xuyên suốt. |
| [`imagegen-frontend-mobile`](.agents/skills/imagegen-frontend-mobile/SKILL.md) | Tạo hình ảnh concept màn hình mobile native đặt trong khung mockup điện thoại sang trọng. |
| [`brandkit`](.agents/skills/brandkit/SKILL.md) | Tạo bảng hướng dẫn thương hiệu (brand guidelines), concept logo, identity deck theo phong cách tối giản, điện ảnh hoặc dark-tech. |

### ⚙️ 6.4. Kiểm soát chất lượng code (Enforcement)
| Skill | Mô tả chức năng |
| :--- | :--- |
| [`full-output-enforcement`](.agents/skills/full-output-enforcement/SKILL.md) | Ngăn chặn hiện tượng AI cắt bớt code hoặc chèn placeholder (như `// code tiếp theo...`), ép AI xuất đầy đủ mã nguồn 100%. |

---

### 💡 Hướng dẫn sử dụng Skill với AI
Khi trò chuyện với AI trong dự án này, bạn có thể kích hoạt skill bằng cách nhắc tên trong prompt:
* *"Hãy dùng skill `design-taste-frontend` để thiết kế trang Landing Page cho dự án."*
* *"Áp dụng `apple-design` để audit lại giao diện component này."*
* *"Dùng `full-output-enforcement` để sinh toàn bộ mã nguồn đầy đủ, không rút gọn."*
# THREETL
