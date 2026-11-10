# Cấu Trúc Nhị Phân Định Dạng PAK & SPR (Kingsoft JX1)

Tài liệu này giải thích chi tiết cấu trúc nhị phân của hai định dạng dữ liệu cốt lõi trong client Võ Lâm Truyền Kỳ: tệp lưu trữ **PAK (`.pak`)** và định dạng ảnh động **SPR (`.spr`)**.

---

## 1. Định Dạng Tệp Lưu Trữ PAK (`.pak`)

Tệp `.pak` là kho chứa nhị phân lưu trữ hàng chục nghìn file tài nguyên con (ảnh SPR, file cấu hình TXT, âm thanh WAV, bản đồ DAT,...).

### 1.1 Cấu Trúc Header (32 bytes đầu tệp)
| Offset | Kích thước | Kiểu dữ liệu | Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `0x00` | 4 bytes | `char[4]` | Ký hiệu nhận dạng (`PACK` hoặc dữ liệu khởi tạo) |
| `0x04` | 4 bytes | `uint32` | **Tổng số file con trong PAK** (`file_count`) |
| `0x08` | 4 bytes | `uint32` | **Vị trí bắt đầu bảng mục lục** (`index_offset`) |
| `0x0C` | 20 bytes | `byte[20]` | Dữ liệu dự phòng / checksum |

### 1.2 Bảng Mục Lục File (File Index Table)
Tại vị trí `index_offset`, bảng mục lục bao gồm `file_count` bản ghi, mỗi bản ghi dài đúng **16 bytes**:

```text
struct PakFileEntry {
    uint32_t hash_id;          // Giá trị Hash 32-bit của đường dẫn tương đối
    uint32_t offset;           // Vị trí bắt đầu dữ liệu nén trong file PAK
    uint32_t uncompressed_sz;  // Kích thước thực tế sau khi giải nén (bytes)
    uint32_t comp_info;        // Thông tin nén (comp_size & is_compressed)
};
```

- **Giải mã `comp_info`**:
  - `comp_size = comp_info & 0x00FFFFFF`: Kích thước khối dữ liệu lưu trong file PAK.
  - `is_compressed = (comp_info >> 24) & 0xFF`: Bằng `0` nếu không nén, khác `0` nếu nén.

### 1.3 Thuật Toán Băm Đường Dẫn Kingsoft (`g_HashString2Id`)
- Game không lưu chuỗi đường dẫn (như `\spr\npcres\man\ma_bd_001_st01.spr`) mà lưu mã hash 32-bit.
- Chuỗi đường dẫn bắt buộc phải được:
  1. Đổi sang chữ thường (`lowercase`).
  2. Bắt đầu bằng dấu gạch chéo ngược `\` (chuẩn Windows path).
- Thuật toán sử dụng một bảng tra cứu tĩnh 1024 giá trị `unsigned long` khởi tạo sẵn. Triển khai chuẩn nằm tại [`scripts/unpack_pak.py`](../scripts/unpack_pak.py) và bản C tốc độ cao tại [`scripts/fast_scanner.c`](../scripts/fast_scanner.c).

### 1.4 Thuật Toán Giải Nén NRV2B
Dữ liệu nén trong file PAK sử dụng thuật toán nén tốc độ cao **UCL NRV2B** (`nrv2b_decompress_8`). Script Python nạp thư viện C qua `ctypes` để giải nén với tốc độ cực nhanh:
- File C / Wrapper: [`scripts/unpack_pak.py`](../scripts/unpack_pak.py).

---

## 2. Định Dạng Ảnh Động SPR (`.spr`)

Tệp `.spr` chứa chuỗi khung hình hoạt họa 2D của nhân vật, quái vật, vũ khí, hiệu ứng chiêu thức hoặc địa hình.

### 2.1 Cấu Trúc Header của SPR
| Offset | Kích thước | Kiểu | Ý nghĩa |
| :--- | :--- | :--- | :--- |
| `0x00` | 4 bytes | `char[4]` | Ký hiệu nhận dạng (bắt đầu bằng `SPR\0`) |
| `0x04` | 2 bytes | `uint16` | Chiều rộng tham chiếu canvas (`gw` - thường là 320) |
| `0x06` | 2 bytes | `uint16` | Chiều cao tham chiếu canvas (`gh` - thường là 320) |
| `0x08` | 2 bytes | `uint16` | Điểm gốc toạ độ X (`off_x` - thường là 160) |
| `0x0A` | 2 bytes | `uint16` | Điểm gốc toạ độ Y (`off_y` - thường là 240) |
| `0x0C` | 2 bytes | `uint16` | **Tổng số khung hình** (`frames`) |
| `0x0E` | 2 bytes | `uint16` | **Số màu trong Palette** (`colors` - tối đa 256) |
| `0x10` | 2 bytes | `uint16` | **Số hướng hiển thị** (`dirs` - thường là 8 hướng) |
| `0x12` | 2 bytes | `uint16` | Tần số trễ giữa các khung hình (`interval`) |
| `0x14` | 12 bytes| `byte[12]`| Dữ liệu phụ |

### 2.2 Bảng Màu Palette
- Nằm ngay sau header tại offset `0x20` (byte 32).
- Kích thước: `colors * 3` bytes.
- Mỗi màu gồm 3 bytes: `R`, `G`, `B` (0-255).
- Màu chỉ số `0` hoặc vùng pixel trong suốt được quy định trong thuật toán vẽ.

### 2.3 Bảng Khung Hình (Frame Offset Table)
- Nằm ngay sau bảng màu Palette: `offset = 32 + colors * 3`.
- Gồm `frames` bản ghi, mỗi bản ghi **8 bytes**:
  - `offset` (uint32): Vị trí bắt đầu của frame tính từ `base_offset` (`base = ftbl + frames * 8`).
  - `length` (uint32): Chiều dài dữ liệu nén của frame.

### 2.4 Cấu Trúc Dữ Liệu Khung Hình (Frame Data)
Dữ liệu của từng frame có thể được nén NRV2B (khi byte đầu của bảng khung hình khác 0) hoặc dạng thô. Khi giải nén, 8 bytes đầu của frame chứa:
- `fw` (int16): Chiều rộng bounding box thực tế của frame ảnh.
- `fh` (int16): Chiều cao bounding box thực tế của frame ảnh.
- `fx` (int16): Toạ độ gốc X so với canvas nhân vật ($320 \times 320$).
- `fy` (int16): Toạ độ gốc Y so với canvas nhân vật ($320 \times 320$).

Dữ liệu pixel sau đó được mã hóa dạng **RLE (Run-Length Encoding)**:
- Đọc cặp 2 bytes `[count, alpha]`.
- Nếu `alpha == 0`: Nhảy qua `count` pixel trong suốt.
- Nếu `alpha != 0`: Đọc liên tiếp `count` bytes tiếp theo, mỗi byte là chỉ số màu tra vào bảng Palette.

### 2.5 Tính Toán Khung Hình Theo Hướng
- Game có 8 hướng chuẩn: `Dir 0` (Nam) đến `Dir 7` (Đông Nam).
- Số khung hình trên mỗi hướng:
  $$\text{Frames Per Direction (fpd)} = \frac{\text{frames}}{\text{dirs}}$$
- Khung hình thứ $f$ của hướng $d$ nằm tại chỉ số:
  $$\text{Index} = d \times \text{fpd} + f$$
- Thông số `fpd` này được script ghi tự động vào `sheetMeta` trong [`character-pixijs/public/assets/catalog.json`](../character-pixijs/public/assets/catalog.json) để PixiJS dựng animation chuẩn xác.
