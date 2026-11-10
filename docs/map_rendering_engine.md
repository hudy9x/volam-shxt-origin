# Động Cơ Render Bản Đồ Isometric (Map Rendering Engine)

Tài liệu này mô tả cấu trúc bản đồ của Võ Lâm Truyền Kỳ và quy trình render bản đồ hoàn chỉnh dạng Isometric $64 \times 32$ từ dữ liệu nhị phân của client.

---

## 1. Kiến Trúc Bản Đồ JX1

- **Hệ toạ độ**: Isometric 2.5D (hình quả trám xiên).
- **Kích thước Tile cơ bản**: $64 \text{ pixel (chiều rộng)} \times 32 \text{ pixel (chiều cao)}$.
- **Đơn vị phân vùng (Region & Cell)**:
  - Bản đồ lớn được chia thành các khu vực (`Region`), mỗi Region gồm lưới các ô nhỏ (`Cell`).
  - Mỗi Cell quản lý các chỉ số:
    1. **Layer Nền đất (Ground Tiles)**: Các mảnh ghép cỏ, đá, đường mòn, mặt nước.
    2. **Layer Vật thể (Object Sprites)**: Nhà cửa, cổng thành, cây cối, cầu cống, tượng đá.
    3. **Layer Chướng ngại vật (Obstacle Flags)**: Xác định vùng nhân vật có thể đi qua, bị chặn, hoặc khu vực an toàn / phi chiến đấu.

---

## 2. Các Tệp Tin Bản Đồ Cốt Lõi

1. **`maps.pak`**:
   - Chứa toàn bộ tile địa hình nền đất và sprite vật thể tĩnh dùng trong cảnh quan.
2. **`Client_VLTK_SHXT/maps/`**:
   - Thư mục chứa cấu hình chi tiết của từng map:
     - `Region_C.dat`: Tệp nhị phân chứa ma trận chỉ số tile của từng region.
     - `map.ini` / `settings/maps.txt`: Danh sách tên bản đồ, kích thước map, toạ độ hồi sinh, điểm truyền tống (teleport), toạ độ NPC.
3. **Minimap**:
   - Bản đồ thu nhỏ 2D được nén trong `maps.pak` phục vụ radar định vị góc trên bên phải màn hình.

---

## 3. Quy Trình Ghép & Render Bản Đồ

Quy trình dựng bản đồ lớn từ tile nhị phân được thực hiện qua các công cụ trong [`scripts/`](../scripts):

```mermaid
flowchart LR
    A["maps.pak & Region_C.dat"] --> B["jx_map.py<br>(Bộ phân tích tile & cell)"]
    B --> C["fast_scanner.dylib<br>(Tăng tốc C đa luồng)"]
    C --> D["render_all_maps_multiprocess.py<br>(Render song song)"]
    D --> E["Ảnh bản đồ hoàn chỉnh<br>(PNG / JPG độ phân giải cao)"]
```

### 3.1 Các Script Bản Đồ Trọng Tâm
- [`scripts/jx_map.py`](../scripts/jx_map.py): Thư viện cốt lõi nạp cấu trúc nhị phân `Region_C.dat`, tính toán phép chiếu toạ độ Isometric và đặt vị trí các sprite.
- [`scripts/render_all_maps_multiprocess.py`](../scripts/render_all_maps_multiprocess.py): Sử dụng `multiprocessing` của Python kết hợp cùng thư viện tăng tốc C [`scripts/fast_scanner.c`](../scripts/fast_scanner.c) để render hàng trăm bản đồ (Biện Kinh, Lâm An, Tương Dương, Phượng Tường, Ba Lăng Huyện,...) trong thời gian ngắn.
- [`scripts/render_stitched_maps.py`](../scripts/render_stitched_maps.py): Ghép các mảnh region thành bản đồ đại cảnh hoàn chỉnh.
- [`scripts/extract_phuong_tuong_assets.py`](../scripts/extract_phuong_tuong_assets.py) & [`scripts/stitch_phuong_tuong.py`](../scripts/stitch_phuong_tuong.py): Bộ công cụ mẫu trích xuất và ghép chi tiết thành trì Phượng Tường.
