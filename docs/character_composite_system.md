# Hệ Thống Ghép Sprite Nhân Vật Đa Lớp (Layered Avatar Compositing)

Tài liệu này giải thích cơ chế ghép hình ảnh nhân vật của Võ Lâm Truyền Kỳ. Nhân vật trong JX1 **không phải là 1 sprite nguyên khối**, mà là một hệ thống ghép từ **10 đến 14 lớp sprite độc lập (layers)** chuyển động đồng bộ theo 8 hướng.

---

## 1. Các Bộ Phận (Part IDs & Sprite Codes)

| Mã Part | Tên Bộ Phận | Tiền tố file | Mô tả & Chức năng |
| :---: | :--- | :---: | :--- |
| `0` | Thân Áo (Body) | `bd` | Trang phục chính, quyết định kiểu dáng áo giáp và quần. |
| `1` | Đầu / Mũ (Head) | `hd` | Khuôn mặt, kiểu tóc hoặc mũ trụ của nhân vật. |
| `2` | Tay Áo Trái (Left Hand) | `lh` | Cánh tay và ống tay áo bên trái. |
| `3` | Tay Áo Phải (Right Hand) | `rh` | Cánh tay và ống tay áo bên phải. |
| `8` | Vũ Khí Trái (Left Weapon) | `lw` | Vũ khí cầm trên tay trái (chỉ dùng cho **Song Binh**). |
| `9` | Vũ Khí Phải (Right Weapon) | `rw` | Vũ khí cầm trên tay phải (đao, kiếm, bổng, thương, chùy,...). |
| `12` | Ngựa Trước (Horse Front) | `hh` | Đầu ngựa, dây cương, chân trước và giáp ngực ngựa. |
| `13` | Thân Ngựa (Horse Mid) | `hb` | Yên ngựa, mình ngựa (vùng nhân vật ngồi lên). |
| `14` | Ngựa Sau (Horse Back) | `ht` | Mông ngựa, đuôi ngựa và chân sau của ngựa. |
| `4` | Phi Phong (Mantle) | `mf` | Áo choàng / cánh bay phía sau lưng nhân vật. |

---

## 2. Quy Tắc Đồng Bộ Tay Áo (Sleeve Synchronization)

> [!CAUTION]
> Khi thay đổi Thân Áo (`bd`), **bắt buộc phải thay đổi đồng thời Tay Trái (`lh`) và Tay Phải (`rh`)** có cùng mã model ID!
> Nếu chỉ đổi thân áo mà giữ nguyên tay áo, nhân vật sẽ bị lỗi đứt gãy khớp tay hoặc lộ da thịt không ăn khớp với trang phục.

---

## 3. Hệ Thống Thứ Tự Vẽ Phân Tầng Z-Order

Thứ tự vẽ layer của nhân vật **thay đổi liên tục theo từng Hướng nhìn (Dir1 -> Dir8) và từng Hành động (Action)**. Quy tắc này được lưu trữ trong:
- Nhân vật Nam: [`Client_VLTK_SHXT/settings/npcres/男主角贴图顺序表.txt`](../Client_VLTK_SHXT/settings/npcres)
- Nhân vật Nữ: [`Client_VLTK_SHXT/settings/npcres/女主角贴图顺序表.txt`](../Client_VLTK_SHXT/settings/npcres)

### 3.1 Ví dụ Điển Hình
- **Khi nhìn Hướng Nam (Dir 1 - Trực diện)**:
  $$\text{Z-Order: } \text{Thân Ngựa } (13) \rightarrow \text{Thân Áo } (0) \rightarrow \text{Đầu } (1) \rightarrow \text{Ngựa Trước } (12) \rightarrow \text{Vũ Khí } (9)$$
  *(Thân ngựa vẽ dưới đùi nhân vật, nhưng đầu ngựa vẽ đè lên chân nhân vật để tạo chiều sâu 3D).*
- **Khi nhìn Hướng Bắc (Dir 5 - Quay lưng)**:
  $$\text{Z-Order: } \text{Vũ Khí } (9) \rightarrow \text{Thân Áo } (0) \rightarrow \text{Phi Phong } (4) \rightarrow \text{Ngựa Sau } (14)$$
  *(Lưng áo và phi phong vẽ đè lên vũ khí và cánh tay).*

### 3.2 Bộ Đọc Z-Order trong Mã Nguồn
Toàn bộ logic Z-order đa hướng được trích xuất tự động thành tệp JSON tại [`character-pixijs/public/assets/zorders.json`](../character-pixijs/public/assets/zorders.json) và áp dụng realtime trong [`character-pixijs/src/renderer/pixi-character.ts`](../character-pixijs/src/renderer/pixi-character.ts).

---

## 4. Bảng Mã Hành Động (Action Codes)

| Hành Động | Trạng Thái Vũ Khí | Mã File SPR | Tên Section Z-Order |
| :--- | :--- | :---: | :--- |
| **Đứng (Stand)** | Tay không | `st01` | `FreeStand1` |
| | Đao / Kiếm / Ám khí | `st04` | `NormalStand1` |
| | Thương / Côn | `st05` | `SpearStand` |
| | Song Binh (Song Đao/Chùy) | `st06` | `DoubleWStand` |
| | Cưỡi Ngựa (Mọi vũ khí) | `rd01` | `RideStand` |
| **Chạy (Move)** | Đi bộ / Chạy bộ | `rn01` - `rn04` | `NormalRun` |
| | Cưỡi ngựa chạy | `hr01` | `RideRun` |
| **Đánh (Attack)** | Quyền cước tay không | `at01` | `FistAttack` |
| | Thương / Côn đâm | `at02` | `SpearAttack` |
| | Đao / Kiếm chém đơn | `at04` | `BladeCut` |
| | **Song Binh (2 tay 2 vũ khí)** | `at06` | `DoubleWPull` |
| | Tấn công trên ngựa | `ha01` | `RideCut` |
| **Bị Thương (Hurt)** | Dưới đất | `ij01` - `ij04` | `Hurt` |
| | Trên ngựa | `hi01` | `RideWound` |

---

## 5. Xử Lý Song Binh (Dual Wielding)

Khi nhân vật trang bị **Song Đao**, **Song Chùy** hoặc **Song Kiếm**:
1. Cần hiển thị đồng thời hai vũ khí:
   - Tay phải (`PART_ID.RIGHT_WEAPON = 9`): Tệp ảnh `weapon_r_{id}_{code}.png`.
   - Tay trái (`PART_ID.LEFT_WEAPON = 8`): Tệp ảnh `weapon_l_{id}_{code}.png`.
2. Hành động tấn công chuyển sang mã `at06` (`DoubleWPull`), đòi hỏi các bộ phận Thân (`bd`), Đầu (`hd`), Tay trái (`lh`), Tay phải (`rh`) đều phải nạp khung hình `at06`.
3. Script trích xuất chuyên dụng: [`scripts/export_dual_and_missing.py`](../scripts/export_dual_and_missing.py).

---

## 6. Phân Biệt Giới Tính (Nam vs Nữ)
- **Nam (Man)**:
  - File SPR bắt đầu bằng `ma_` (ví dụ `ma_bd_001_st01.spr`).
  - Thư mục nạp: `\spr\npcres\man\`.
  - Cấu hình: `男主角*.txt`.
- **Nữ (Woman)**:
  - File SPR bắt đầu bằng `fm_` (ví dụ `fm_bd_001_st01.spr`).
  - Thư mục nạp: `\spr\npcres\woman\`.
  - Cấu hình: `女主角*.txt`.

---

## 7. Khung Cắt Chuẩn (Crop Box & Coordinate Alignment)
- Khung hình gốc của game có kích thước canvas là $320 \times 320$ pixel với gốc toạ độ chân nhân vật tại $(160, 240)$.
- Để tối ưu hóa bộ nhớ WebGL và giảm dung lượng tải mạng, công cụ cắt gọn bounding box chuẩn:
  - Toạ độ cắt: `X1 = 70`, `Y1 = 45`.
  - Chiều rộng và chiều cao: `Width = 180`, `Height = 180`.
  - Toàn bộ spritesheet của nhân vật trong PixiJS đều đồng nhất ở kích thước frame $180 \times 180$ pixel.
