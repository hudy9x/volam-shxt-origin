# Tổng Quan Client Võ Lâm Truyền Kỳ - Sơn Hà Xã Tắc (SHXT)

Tài liệu này cung cấp cái nhìn tổng quan về kiến trúc, cấu trúc tệp tin và các quy ước nền tảng của bản client **Võ Lâm Truyền Kỳ 1 (Kiếm Hiệp Tình Duyên Online / JX1)**, phiên bản **Sơn Hà Xã Tắc (SHXT)** nằm tại thư mục [`Client_VLTK_SHXT/`](../Client_VLTK_SHXT).

---

## 1. Bản Chất Kiến Trúc Game JX1
- **Thể loại**: MMORPG kiếm hiệp 2.5D Isometric (góc nhìn xiên 45 độ, lưới isometric $64 \times 32$ pixel).
- **Engine**: Swordman Online Engine do Kingsoft phát triển (C/C++).
- **Hệ thống hiển thị**: Đồ họa Sprite 2D phân tầng (Multi-layer 2D Sprites) với bảng màu Indexed 256 màu (8-bit Palette per Sprite).
- **Hệ thống hướng di chuyển**: 8 hướng chuẩn (Nam, Tây Nam, Tây, Tây Bắc, Bắc, Đông Bắc, Đông, Đông Nam).

---

## 2. Cấu Trúc Thư Mục [`Client_VLTK_SHXT/`](../Client_VLTK_SHXT)

```text
Client_VLTK_SHXT/
├── package.ini                # Cấu hình danh sách & thứ tự ưu tiên các tệp PAK
├── data/                      # Chứa 29 tệp lưu trữ nhị phân nén (.pak)
│   ├── spr.pak                # Dữ liệu sprite gốc (nhân vật, trang bị cơ bản, NPC)
│   ├── skills.pak             # Hiệu ứng chiêu thức võ công
│   ├── maps.pak               # Dữ liệu địa hình, lưới tile, chướng ngại vật
│   ├── ui.pak                 # Giao diện người dùng (khung hình, nút bấm, icon)
│   ├── update.pak             # Bản cập nhật vá lỗi
│   ├── update01.pak ... 05.pak# Các bản cập nhật phiên bản đầu
│   └── updatejx01.pak ... 14.pak # Các bản cập nhật tính năng mở rộng (120, 150, thần thú)
├── settings/                  # Toàn bộ cấu hình hệ thống bằng bảng TSV (Tab-separated)
│   ├── item/                  # Cấu hình thuộc tính trang bị (vũ khí, áo, nón, ngựa, bí kíp)
│   │   ├── horse.txt          # Danh sách chiến mã (cấp độ, tên gọi, chỉ số)
│   │   ├── horseres.txt       # Ánh xạ item chiến mã sang mã model hiển thị
│   │   ├── armor.txt / helm.txt / weapon.txt # Cấu hình trang phục và vũ khí
│   │   └── ...
│   ├── npcres/                # Định nghĩa tài nguyên đồ họa cho nhân vật và NPC
│   │   ├── 男主角*.txt         # File cấu hình mô hình, bộ phận nhân vật Nam
│   │   ├── 女主角*.txt         # File cấu hình mô hình, bộ phận nhân vật Nữ
│   │   ├── 男主角贴图顺序表.txt # Bảng Z-Order quyết định thứ tự vẽ layer của Nam
│   │   ├── 女主角贴图顺序表.txt # Bảng Z-Order quyết định thứ tự vẽ layer của Nữ
│   │   └── ...
│   ├── skills.txt             # Định nghĩa toàn bộ chiêu thức võ công 10 môn phái
│   ├── faction.txt            # Thông số 10 môn phái (Thiếu Lâm, Thiên Vương, Đường Môn,...)
│   └── ...
└── maps/                      # Bản đồ thô, tệp toạ độ và chướng ngại vật (.dat)
```

---

## 3. Cơ Chế Nạp Dữ Liệu & Độ Ưu Tiên (`package.ini`)

Game sử dụng cơ chế nạp đè theo danh sách thứ tự được quy định trong tệp [`Client_VLTK_SHXT/package.ini`](../Client_VLTK_SHXT/package.ini):
- Tệp PAK có chỉ số nhỏ hơn (`0=ui.pak`, `2=updatejx14.pak`,...) có độ ưu tiên **cao hơn**.
- Tệp PAK có chỉ số lớn hơn (`23=spr.pak`, `25=maps.pak`,...) là tài nguyên gốc nền tảng.
- Khi tìm kiếm một file (ví dụ `\spr\npcres\man\ma_hh_030_rd01.spr`), hệ thống sẽ quét từ PAK cập nhật mới nhất xuống cũ dần. Nếu tìm thấy ở `updatejx05.pak`, file đó sẽ đè lên phiên bản trong `spr.pak`.

> [!IMPORTANT]
> Khi viết bất kỳ script nào đọc tài nguyên client, luôn phải quét các file PAK theo thứ tự đảo ngược (reverse) của danh sách ưu tiên, để bản ghi ở các PAK cập nhật sau cùng đè lên bản ghi ở PAK cũ hơn.

---

## 4. Quy Ước Bảng Mã Văn Bản (Encoding Conventions)

Game VLTK SHXT sử dụng hỗn hợp hai bảng mã khác nhau tùy theo loại dữ liệu:

1. **Bảng mã GBK / CP936 (Tiếng Trung giản thể)**:
   - Áp dụng cho: Tên file mã nguồn gốc trong hệ điều hành, tên section cấu hình trong `settings/npcres/` (ví dụ `男主角贴图顺序表.txt`, `男主角躯体.txt`).
   - Trên macOS / Linux, hệ thống file có thể biểu diễn tên file này dưới dạng Unicode mojibake (ví dụ `ÄÐÖ÷½Ç...`). Để giải mã chính xác trong Python:
     ```python
     unicodedata.normalize('NFC', filename).encode('latin1').decode('gbk')
     ```

2. **Bảng mã TCVN3 / ABC (Tiếng Việt 1-byte cũ)**:
   - Áp dụng cho: Toàn bộ nội dung văn bản tiếng Việt hiển thị trong game (tên trang bị, mô tả vật phẩm, tên NPC trong `settings/item/*.txt`, `settings/skills.txt`).
   - Các ký tự tiếng Việt có dấu được mã hóa thành các byte từ `0x80` đến `0xFF` (ví dụ: `Li謙 Ho祅g M ` chính là `Liệt Hoàng Mã`).
   - Cần sử dụng bảng tra cứu ánh xạ byte TCVN3 sang Unicode utf-8 khi trích xuất dữ liệu để người dùng và giao diện web đọc được tiếng Việt chuẩn.

---

## 5. Tài Liệu Chi Tiết Đi Kèm
- [`docs/file_formats_pak_spr.md`](file_formats_pak_spr.md): Giải mã cấu trúc nhị phân của tệp PAK và SPR.
- [`docs/character_composite_system.md`](character_composite_system.md): Cơ chế ghép Sprite nhân vật đa lớp và bảng Z-Order.
- [`docs/equipment_and_horses_catalog.md`](equipment_and_horses_catalog.md): Thống kê trang bị, vũ khí, áo nón và thú cưỡi.
- [`docs/map_rendering_engine.md`](map_rendering_engine.md): Cơ chế đọc và ghép bản đồ Isometric JX1.
- [`docs/tooling_and_scripts_guide.md`](tooling_and_scripts_guide.md): Hướng dẫn sử dụng toàn bộ công cụ trong thư mục [`scripts/`](../scripts).
