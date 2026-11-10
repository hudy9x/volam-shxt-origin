# Hệ Thống Tài Liệu Kỹ Thuật Võ Lâm Truyền Kỳ (SHXT)

Thư mục [`docs/`](.) chứa toàn bộ kiến thức chuyên sâu và tài liệu kỹ thuật được tổng hợp từ quá trình dịch ngược, trích xuất và tái hiện đồ họa của client game **Võ Lâm Truyền Kỳ 1 (Sơn Hà Xã Tắc / JX1)**.

---

## 📚 Mục Lục Tài Liệu

1. **[Tổng Quan Client VLTK SHXT](overview_vltk_client.md)**
   - Bản chất kiến trúc game 2.5D Isometric.
   - Cấu trúc thư mục client (`Client_VLTK_SHXT/data`, `settings/`, `maps/`).
   - Cơ chế nạp tài nguyên đè theo độ ưu tiên trong `package.ini`.
   - Quy ước hai bảng mã văn bản: **GBK** (tên file/section) và **TCVN3** (nội dung tiếng Việt).

2. **[Cấu Trúc Nhị Phân Định Dạng PAK & SPR](file_formats_pak_spr.md)**
   - Định dạng tệp nén `.pak`: Header, cấu trúc mục lục, thuật toán băm chuỗi đường dẫn Kingsoft `g_HashString2Id`, thuật toán giải nén UCL NRV2B.
   - Định dạng ảnh hoạt họa `.spr`: Cấu trúc Header, bảng màu 8-bit Palette, bảng frame offset, nén RLE theo hàng, khung bounding box `fw, fh, fx, fy` và công thức tính frame theo hướng `fpd`.

3. **[Hệ Thống Ghép Sprite Nhân Vật Đa Lớp](character_composite_system.md)**
   - Hệ thống 10 – 14 layers bộ phận (`bd`, `hd`, `lh`, `rh`, `rw`, `lw`, `hh`, `hb`, `ht`, `mf`).
   - Quy tắc bắt buộc đồng bộ ống tay áo (`lh`, `rh`) khi đổi áo (`bd`).
   - Bảng thứ tự vẽ Z-Order phụ thuộc vào 8 hướng và từng hành động (`男主角贴图顺序表.txt` / `女主角贴图顺序表.txt`).
   - Bảng mã hành động: `st01`-`st06` (đứng), `rn01`-`rn04` (chạy), `at01`-`at06` (đánh), `ij01`-`ij04` (bị thương), `rd01`, `hr01`, `ha01`, `hi01` (ngựa).
   - Cơ chế cầm 2 vũ khí (Song Binh) và hành động `at06` (`DoubleWPull`).
   - Phân biệt giới tính Nam (`ma_`) và Nữ (`fm_`).

4. **[Danh Mục Trang Bị, Vũ Khí & Thú Cưỡi](equipment_and_horses_catalog.md)**
   - Hệ thống 8 dòng vũ khí (Kiếm, Đao, Thương, Côn, Chùy, Song Binh, Ám Khí, Tay Không) từ Cấp 1 đến Cấp 10 (Hoàng Kim).
   - Phẩm cấp Áo và Mũ từ Cấp 1 đến Cấp 10.
   - Bảng tra cứu toàn diện 28 thú cưỡi từ **Cấp 20 đến Cấp 150+** và Thần Thú Cấp 180 (vị trí file trong `updatejx14`, `updatejx11`, `updatejx10`, `updatejx05`, `update03`, `update02`, `spr.pak`).

5. **[Động Cơ Render Bản Đồ Isometric](map_rendering_engine.md)**
   - Kiến trúc lưới Isometric $64 \times 32$ pixel.
   - Cấu trúc Region, Cell, Layer nền đất (ground), Layer vật thể (objects) và Layer chướng ngại vật (obstacles) từ `Region_C.dat`.
   - Pipeline ghép và render bản đồ hoàn chỉnh đa tiến trình.

6. **[Cẩm Nang Công Cụ & Scripts](tooling_and_scripts_guide.md)**
   - Danh sách phân loại và hướng dẫn sử dụng toàn bộ script trong [`scripts/`](../scripts).
   - Hướng dẫn vận hành ứng dụng xem trước WebGL tại [`character-pixijs/`](../character-pixijs).

7. **[Danh Mục & Phân Loại 29 Tệp PAK](pak_files_catalog.md)**
   - Thống kê toàn diện 29 tệp `.pak` trong thư mục `Client_VLTK_SHXT/data/`.
   - Bảng tra cứu dung lượng, số lượng file con và vai trò chi tiết theo thứ tự ưu tiên nạp `package.ini`.
   - Phân loại theo 5 nhóm chức năng: Giao diện, Đồ họa cốt lõi, Bản đồ, Chuỗi cập nhật JX và Chuỗi cập nhật cổ điển.
