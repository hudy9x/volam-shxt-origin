# Cẩm Nang Công Cụ & Scripts Xử Lý (Tooling & Scripts Guide)

Thư mục [`scripts/`](../scripts) chứa toàn bộ các công cụ viết bằng Python và C nhằm phân tích, trích xuất, giải nén và render tài nguyên từ client game.

---

## 1. Phân Loại Bộ Công Cụ

```text
scripts/
├── [Nhóm 1: Giải Nén & Phân Tích Nhị Phân]
│   ├── unpack_pak.py              # Bộ giải mã PAK và nén NRV2B qua ctypes
│   ├── fast_scanner.c / .dylib    # Thư viện C băm chuỗi và quét PAK cực nhanh
│   ├── test_hash.c / test_hash    # Kiểm tra thuật toán mã hoá g_HashString2Id
│   └── investigate_sprites.py     # Quét và thống kê toàn bộ sprite trong các PAK
│
├── [Nhóm 2: Xuất Assets Cho PixiJS & Web]
│   ├── build_full_pixi_assets.py  # Xuất toàn diện Nam & Nữ (Áo, Mũ, Vũ khí 8 phái, Ngựa)
│   ├── export_extended_horses.py  # Xuất toàn bộ 28 Chiến Mã & Thần Thú Cấp 20 -> 150+
│   ├── export_dual_and_missing.py # Trích xuất chuyên sâu Song Binh (2 tay 2 vũ khí)
│   ├── extract_remaining_parts.py # Trích xuất bổ sung áo giáp, mũ trụ, phi phong
│   └── build_pixi_assets.py       # Phiên bản xuất sprite cơ bản ban đầu
│
├── [Nhóm 3: Động Cơ Bản Đồ & Render Map]
│   ├── jx_map.py                  # Thư viện cốt lõi nạp Region_C.dat & tile isometric
│   ├── render_all_maps_multiprocess.py # Render hàng trăm bản đồ song song đa tiến trình
│   ├── build_map_rendered.py      # Sinh danh mục bản đồ đã render
│   ├── extract_map_images.py      # Trích xuất minimap và ảnh bản đồ gốc
│   ├── render_stitched_maps.py    # Ghép các mảnh region thành bản đồ khổ lớn
│   ├── extract_phuong_tuong_assets.py # Trích xuất tài nguyên thành Phượng Tường
│   └── stitch_phuong_tuong.py     # Ghép hoàn chỉnh bản đồ Phượng Tường
│
└── [Nhóm 4: Phân Tích & Báo Cáo Kỹ Năng]
    ├── build_multistage_report.py # Phân tích hiệu ứng chiêu thức (Tụ -> Bắn -> Nổ)
    ├── generate_report_120_150.py # Trích xuất và lập báo cáo kỹ năng cấp 120 & 150
    └── update_120_animations.py   # Cập nhật ảnh động GIF cho chiêu 120
```

---

## 2. Hướng Dẫn Sử Dụng Chi Tiết Từng Công Cụ

### 2.1 [`unpack_pak.py`](../scripts/unpack_pak.py)
- **Mục đích**: Chứa hai hàm hạt nhân `g_HashString2Id` và `get_decompressor` (NRV2B). Mọi script khác đều import thư viện này.
- **Sử dụng độc lập**:
  ```bash
  python3 scripts/unpack_pak.py Client_VLTK_SHXT/data/spr.pak output_folder/
  ```

### 2.2 [`export_extended_horses.py`](../scripts/export_extended_horses.py)
- **Mục đích**: Nạp chỉ mục đa PAK theo thứ tự ưu tiên của `package.ini`, trích xuất 28 loại chiến mã và thần thú (Cấp 20, 40, 60, 80, 120, 130, 150, 180), tạo icon $54 \times 54$ và cập nhật [`character-pixijs/public/assets/catalog.json`](../character-pixijs/public/assets/catalog.json).
- **Chạy lệnh**:
  ```bash
  python3 scripts/export_extended_horses.py
  ```

### 2.3 [`export_dual_and_missing.py`](../scripts/export_dual_and_missing.py)
- **Mục đích**: Xử lý riêng cho hệ vũ khí kép (**Song Binh**: Song Đao, Song Chùy, Song Kiếm). Xuất đồng thời 2 file spritesheet tay trái (`weapon_l`) và tay phải (`weapon_r`), kèm theo động tác tấn công `at06` (`DoubleWPull`).
- **Chạy lệnh**:
  ```bash
  python3 scripts/export_dual_and_missing.py
  ```

### 2.4 [`build_full_pixi_assets.py`](../scripts/build_full_pixi_assets.py)
- **Mục đích**: Bộ xuất toàn diện nạp cả nhân vật Nam (`ma_`) và Nữ (`fm_`), toàn bộ 8 dòng vũ khí cấp 1-10, áo mũ cấp 1-10, bảng Z-Order và cắt khung chuẩn $180 \times 180$ pixel.
- **Chạy lệnh**:
  ```bash
  python3 scripts/build_full_pixi_assets.py
  ```

### 2.5 [`render_all_maps_multiprocess.py`](../scripts/render_all_maps_multiprocess.py)
- **Mục đích**: Render toàn bộ bản đồ thế giới của game bằng cách tận dụng toàn bộ số nhân CPU máy tính.
- **Biên dịch thư viện C trước khi chạy** (nếu chưa có `fast_scanner.dylib`):
  ```bash
  gcc -O3 -shared -fPIC scripts/fast_scanner.c -o scripts/fast_scanner.dylib
  python3 scripts/render_all_maps_multiprocess.py
  ```

---

## 3. Ứng Dụng Xem Trước Trực Quan: [`character-pixijs/`](../character-pixijs)
- Giao diện web chạy bằng Vite + PixiJS v8 + TypeScript:
  - Khởi động dev server:
    ```bash
    cd character-pixijs && npm run dev
    ```
  - Truy cập: `http://localhost:5174/`
  - Các tính năng chính:
    - Đổi giới tính realtime (Nam / Nữ) với icon và z-order tương ứng.
    - Bộ chọn trang bị phân tầng (Áo, Mũ, Ngựa, Vũ khí 8 phái với chip lọc phẩm cấp).
    - Bộ lọc danh mã: Cấp 20-60, Cấp 80, Cấp 100-130, Cấp 150, Thần Thú Cấp 180.
    - Điều khiển 8 hướng nhìn và 4 hành động (Đứng, Chạy, Đánh, Bị thương).
    - Bảng thanh tra layer (Layer Inspector) hiển thị độ sâu Z-order thời gian thực.
