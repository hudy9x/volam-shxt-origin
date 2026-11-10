# Các Mốc Tốc Độ Di Chuyển & Tốc Độ Xuất Chiêu (Speed Breakpoints)

Tài liệu này giải thích bản chất engine **18 Frames/Giây** của Võ Lâm Truyền Kỳ và lý do vì sao chỉ số Tốc độ xuất chiêu, Tốc độ đánh và Tốc độ di chuyển lại vận hành theo **Các Mốc (Breakpoints)** chứ không tăng tuyến tính liên tục.

---

## 1. Nguồn Gốc Kỹ Thuật: Chu Kỳ 18 FPS Của Kingsoft

Trong tệp cấu hình nền tảng [`Client_VLTK_SHXT/settings/npc/player/basevalue.ini`](../Client_VLTK_SHXT/settings/npc/player/basevalue.ini):
- `AttackFrame = 18` (Chu kỳ xuất chiêu tấn công cơ bản là 18 frames).
- `CastFrame = 18` (Chu kỳ niệm phép nội công cơ bản là 18 frames).
- **1 giây trong thế giới game tương ứng với đúng 18 khung hình (18 ticks)**.

> [!IMPORTANT]
> Vì màn hình chỉ có thể vẽ khung hình theo **số nguyên** (18, 17, 16, 15, 14... frames), một đòn đánh **không thể diễn ra trong 15.4 frames**.
> Do đó, nếu bạn tăng tốc độ đánh từ 21% lên 25%, số frame thực tế vẫn bị giữ nguyên ở **15 frames**! Đòn đánh chỉ thực sự nhanh hơn khi bạn chạm tới mốc tiếp theo (**29%** để nhảy xuống **14 frames**).

---

## 2. Bảng Các Mốc Tốc Độ Đánh & Xuất Chiêu Chuẩn (ASPD Breakpoints)

Công thức tính số khung hình thực tế của một lần ra đòn:
$$\text{Số Frames Hoạt Họa} = \left\lfloor \frac{18 \times 100}{100 + \text{Tốc Độ \%}} \right\rfloor$$

| Mốc Tốc Đánh / Xuất Chiêu (`%`) | Số Frames Mỗi Lần Ra Đòn | Tốc Độ Thực Tế (Số đòn / 1 giây) | Nhận Xét & Ứng Dụng Thực Chiến |
| :---: | :---: | :---: | :--- |
| **0% – 5%** | **18 frames** | 1.00 đòn/giây | Tốc độ xuất chiêu cơ bản khi không mang trang bị tăng tốc. |
| **6% – 12%** | **17 frames** | 1.06 đòn/giây | Mốc khởi đầu sơ cấp. |
| **13% – 20%** | **16 frames** | 1.13 đòn/giây | Đạt được khi có bao tay hoặc vũ khí tốc độ 10-20%. |
| **21% – 28%** | **15 frames** | 1.20 đòn/giây | Mốc phổ biến ở giai đoạn trung cấp. |
| **29% – 38%** | **14 frames** | 1.29 đòn/giây | Mốc vàng cho các phái nội công (Dây chuyền 20% + Chiêu thức 10%). |
| **39% – 50%** | **13 frames** | 1.38 đòn/giây | Tăng tốc rõ rệt, đòn đánh dồn dập hơn. |
| **51% – 64%** | **12 frames** | 1.50 đòn/giây | Ra đòn nhanh hơn 50% so với tốc độ gốc. |
| **65% – 80%** | **11 frames** | 1.64 đòn/giây | Mốc tiêu chuẩn của các cao thủ PK Ngoại công (Vũ khí 30% + Bao tay 30% + Skill). |
| **81% – 100%** | **10 frames** | 1.80 đòn/giây | Thiên Vương / Thiếu Lâm đạt mốc này sẽ chém/đâm đối thủ không kịp phản ứng. |
| **101% – 125%** | **9 frames** | 2.00 đòn/giây | **Chính xác 2 đòn trong 1 giây**. Ngưỡng sức mạnh bùng nổ của Thiên Vương Thương. |
| **126% – 158%** | **8 frames** | 2.25 đòn/giây | Yêu cầu trang bị Hoàng Kim, hỗ trợ từ Nga My/Côn Lôn. |
| **159%+** | **7 frames** | 2.57 đòn/giây | Ngưỡng trần tối đa của engine game. |

---

## 3. Hệ Thống Tốc Độ Di Chuyển (Movement Speed)

### 3.1 Tốc Độ Cơ Bản Của Nhân Vật
Trong [`basevalue.ini`](../Client_VLTK_SHXT/settings/npc/player/basevalue.ini):
- `WalkSpeed = 5` (Tốc độ đi bộ khi bấm Shift hoặc đi dạo trong thành).
- `RunSpeed = 10` (Tốc độ chạy bộ bình thường dưới đất).

### 3.2 Tác Động Của Giày Dép
- Giày là trang bị duy nhất mang dòng **Tốc độ di chuyển +%** (`fastwalkrun_p`).
- Các mốc giày phổ biến:
  - Giày Cấp 1 – 4: +20% đến +25%.
  - Giày Cấp 5 – 7: +28% đến +32%.
  - Giày Cấp 8 – 10 (Đồ Xanh Cực Phẩm): **+36% đến +40% Tốc chạy**.

### 3.3 Tác Động Của Thú Cưỡi (Chiến Mã)
Khi cưỡi ngựa, tốc độ di chuyển của nhân vật được nhân theo phẩm cấp của thú cưỡi:
- **Ngựa Cấp 20 (Liệt Mã)**: +20% đến +30% tốc độ.
- **Ngựa Cấp 40 – 60 (Đại Uyển, Xích Ký)**: +40% đến +50% tốc độ.
- **Ngựa Cấp 80 (Chiếu Dạ, Tuyệt Ảnh, Ô Vân, Đích Lô)**: **+70% đến +80% tốc độ**.
- **Ngựa Cấp 120 – 150 (Bôn Tiêu, Phiên Vũ, Ngự Phong, Truy Điện, Lưu Tinh)**: **+100% tốc độ di chuyển** (chạy nhanh gấp đôi nhân vật đi bộ!).

### 3.4 Kỹ Năng Bổ Trợ Tốc Độ Di Chuyển Cực Đại
Một số môn phái sở hữu bùa chú hoặc kỹ năng tăng tốc chạy có thể cộng dồn vượt ngưỡng:
1. **Thê Vân Tung (Võ Đang)**: Khinh công huyền thoại tăng tốc độ di chuyển tức thời.
2. **Lưu Thủy (Nga My)**: Aura tăng tốc chạy cho toàn bộ đồng đội trong tổ đội.
3. **Thanh Phong Phù (Côn Lôn)**: Bùa chú tăng tốc độ di chuyển lên tới 60-80%.
4. **Mê Tung Ảo Ảnh (Đường Môn)**: Tăng tốc cực nhanh để giữ cự ly bắn tỉa thả diều.
5. **Tiếu Ngạo Giang Hồ (Cái Bang)**: Tăng tốc độ và độ né tránh khi áp sát mục tiêu.
