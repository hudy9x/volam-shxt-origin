# Danh Mục Trang Bị, Vũ Khí & Thú Cưỡi (Equipment Catalog)

Tài liệu này hệ thống hóa toàn bộ các dòng trang bị, phẩm cấp và danh mục thú cưỡi trong Võ Lâm Truyền Kỳ SHXT đã được trích xuất và hỗ trợ trong ứng dụng PixiJS.

---

## 1. Hệ Thống 8 Dòng Vũ Khí (Weapons)

Vũ khí trong VLTK được chia làm 8 dòng võ phái chính, trải dài từ Cấp 1 (Sơ cấp) đến Cấp 10 (Hoàng Kim môn phái):

| Dòng Vũ Khí | Mã Danh Mục | Kiểu Hoạt Họa | Môn Phái Tiêu Biểu |
| :--- | :---: | :---: | :--- |
| **Kiếm** | `kiem` | `short` | Võ Đang (Khí/Kiếm), Côn Lôn (Kiếm), Nga My (Kiếm), Hoa Sơn |
| **Đao** | `dao` | `short` | Thiếu Lâm (Đao), Thiên Nhẫn (Đao), Côn Lôn (Đao), Thúy Yên (Đao) |
| **Thương** | `thuong` | `polearm` | Thiên Vương (Thương), Thiên Nhẫn (Thương) |
| **Côn / Bổng** | `bong` | `polearm` | Thiếu Lâm (Côn), Cái Bang (Bổng) |
| **Chùy** | `chuy` | `short` | Thiên Vương (Chùy) |
| **Song Binh** | `songbinh` | `dual` | Thúy Yên (Song Đao), Thiên Vương (Song Chùy/Đao) |
| **Ám Khí** | `amkhi` | `short` | Đường Môn (Phi Đao, Tụ Tiễn, Phi Tiêu) |
| **Tay Không** | `taykhong` | `bare` | Thiếu Lâm (Quyền), Cái Bang (Chưởng), Nga My (Chưởng) |

### 1.1 Phân Phẩm Cấp Vũ Khí
- **Cấp 1 – 3 (Sơ Cấp)**: Mộc Kiếm, Thiết Đao, Trúc Bổng, Bách Luyện Thương,...
- **Cấp 4 – 6 (Trung Cấp)**: Thanh Phong Kiếm, Liễu Diệp Đao, Hắc Thiết Bổng, Lượng Ngân Thương,...
- **Cấp 7 – 9 (Cao Cấp)**: Huyền Thiết Kiếm, Trảm Mã Đao, Phục Ma Bổng, Du Long Thương,...
- **Cấp 10 (Cực Phẩm / Hoàng Kim)**: Ỷ Thiên Kiếm, Đồ Long Đao, Đả Cẩu Bổng, Hám Thiên Khôi Tinh Chùy,...

---

## 2. Hệ Thống Áo Giáp & Mũ Trụ (Armors & Helms)

- **Phân loại**:
  - `Cấp 1 – 3`: Vải thô, áo da, sơ nhập đạo y.
  - `Cấp 4 – 6`: Áo gấm, xích đồng giáp, chiến y trung cấp.
  - `Cấp 7 – 9`: Bạch kim giáp, huyền thiết chiến giáp, dạ xoa chiến bào.
  - `Cấp 10 & Hoàng Kim`: Tứ Không Giáp, Cửu Vĩ Bạch Hồ Bào, Hoàng Kim Chiến Giáp.
- Toàn bộ thân áo khi trang bị đều tự động gắn kết với cặp ống tay tương ứng (`lh` và `rh`).

---

## 3. Danh Mục Chiến Mã & Thần Thú (Level 20 $\rightarrow$ 150+)

Hệ thống thú cưỡi được phân bổ qua nhiều tệp PAK cập nhật khác nhau trong client:

### 3.1 Bảng Tra Cứu Toàn Diện

| Phẩm Cấp | Mã ID | Tên Thú Cưỡi | File PAK Chứa Dữ Liệu | Mô Tả & Ý Nghĩa |
| :---: | :---: | :--- | :--- | :--- |
| **Cấp 20** | `009` | **Liệt Bạch Mã** | `spr.pak` | Ngựa trắng sơ nhập, thích hợp cho tân thủ. |
| **Cấp 20** | `010` | **Liệt Hoàng Mã** | `spr.pak` | Ngựa vàng dẻo dai, bước chạy bền bỉ. |
| **Cấp 40** | `005` | **Đại Uyển Hắc Mã** | `spr.pak` | Hắc Kỳ mã cơ bắp cuồn cuộn. |
| **Cấp 40** | `006` | **Đại Uyển Hoàng Mã**| `spr.pak` | Hoàng Phiêu tuấn mã Tây Vực. |
| **Cấp 40** | `008` | **Đại Uyển Hồng Mã** | `spr.pak` | Hồng Ly bảo mã bờm đỏ thắm. |
| **Cấp 60** | `007` | **Xích Ký** | `spr.pak` | Chiến mã phi tốc xông pha trận mạc. |
| **Cấp 60** | `004` | **Hoa Lưu** | `spr.pak` | Bảo mã bờm vàng óng ánh dũng mãnh. |
| **Cấp 80** | `001` | **Chiếu Dạ Ngọc Sư Tử**| `spr.pak` | Bạch mã thần tốc phi nhanh như chớp giật. |
| **Cấp 80** | `002` | **Tuyệt Ảnh** | `spr.pak` | Toàn thân đen tuyền, phi nhanh không lưu lại bóng. |
| **Cấp 80** | `003` | **Ô Vân Đạp Tuyết** | `spr.pak` | Hắc mã bốn móng trắng như tuyết, chiến mã danh tiếng. |
| **Cấp 80** | `011` | **Đích Lô** | `update03.pak` | Trán có đốm trắng, danh mã cứu chúa Lưu Bị qua suối Đàn Khê. |
| **Cấp 120**| `012` | **Bôn Tiêu** | `update03.pak` | Thần mã truyền thuyết đạp mây rẽ gió, tăng kháng tính cao. |
| **Cấp 130**| `014` | **Xích Long Câu** | `update02.pak` | Huyết hồng bảo mã, khí phách uy nghiêm lẫm liệt. |
| **Cấp 130**| `017` | **Du Huy** | `update02.pak` | Thần câu ánh hoàng kim, cước bộ phiêu dật như mây. |
| **Cấp 150**| `013` | **Phiên Vũ** | `update03.pak` | Đệ nhất danh mã giang hồ, bạt phong trác tuyệt. |
| **Cấp 150**| `030` | **Ngự Phong** | `updatejx05.pak` | Lướt gió ngự phong, phi vân cái thế. |
| **Cấp 150**| `031` | **Truy Điện** | `updatejx05.pak` | Tốc độ như điện xẹt, thần uy vô song. |
| **Cấp 150**| `032` | **Lưu Tinh** | `updatejx05.pak` | Thoắt ẩn thoắt hiện như sao băng rơi xuống trần gian. |
| **Cấp 180**| `033` | **Kim Mao Sư Thần** | `updatejx10.pak` | Sư tử hoàng kim uy nghiêm bễ nghễ thiên hạ. |
| **Cấp 180**| `035` | **Kim Tinh Bạch Hổ**| `updatejx11.pak` | Cọp trắng oai hùng, thần thú chí tôn vạn linh. |
| **Cấp 180**| `036` | **Long Tinh Hắc Hổ**| `updatejx11.pak` | Hắc mãnh hổ sát khí trùng thiên bách chiến bách thắng. |
| **Cấp 180**| `037` | **Hỏa Tinh Kim Hổ** | `updatejx11.pak` | Mãnh hổ hoàng kim rực lửa trác tuyệt. |
| **Cấp 180**| `038` | **Thần Thú Linh Lộc**| `updatejx11.pak` | Linh thú cát tường ngàn năm mang lại điềm lành. |
| **Cấp 180**| `039` | **Bích Thủy Thần Câu**| `updatejx14.pak` | Thần mã lam sắc lướt sóng như bay. |
| **Cấp 180**| `040` | **Tử Long Chiến Mã** | `updatejx14.pak` | Chiến mã tím tôn quý vương giả. |
| **Cấp 180**| `041` | **Hỏa Diệm Chiến Mã**| `updatejx14.pak` | Bừng sáng lửa thiêng chiến trường. |
| **Cấp 180**| `042` | **Hàn Băng Thần Mã** | `updatejx14.pak` | Thần mã băng tuyết hàn khí ngút ngàn. |

### 3.2 Quy Cách File Động Tác Của Ngựa
Mỗi loại thú cưỡi bao gồm 3 bộ phận $\times$ 4 động tác = **12 spritesheets**:
- `horse_front_{id}_{code}.png` (`hh`)
- `horse_mid_{id}_{code}.png` (`hb`)
- `horse_back_{id}_{code}.png` (`ht`)
- Mã động tác: `rd01` (đứng), `hr01` (chạy), `ha01` (tấn công), `hi01` (trúng đòn).
- Script trích xuất: [`scripts/export_extended_horses.py`](../scripts/export_extended_horses.py).
