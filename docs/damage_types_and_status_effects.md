# Phân Loại Sát Thương & Hiệu Ứng Trạng Thái (Damage Types & Status Effects)

Tài liệu này giải thích chi tiết bản chất toán học và cơ chế vận hành của **5 loại sát thương** và các **hiệu ứng trạng thái khống chế** đi kèm trong Võ Lâm Truyền Kỳ SHXT.

---

## 1. 5 Loại Sát Thương Cơ Bản

Hệ thống sát thương trong game được chia làm 5 loại tương ứng với các nguyên tố tự nhiên và hệ ngũ hành:

```text
Sát Thương = Sát Thương Vật Lý + Sát Thương Băng + Sát Thương Lôi + Sát Thương Hỏa + Sát Thương Độc
```

| Loại Sát Thương | Hệ Ngũ Hành | Dạng Tác Động | Hiệu Ứng Đi Kèm | Thuộc Tính Kháng Tương Ứng |
| :--- | :---: | :--- | :--- | :--- |
| **Sát Thương Vật Lý** | Trung tính / Kim | Trực tiếp tức thời | **Thọ thương (Co giật)** | Kháng Vật Lý (`PhysicsRes`) |
| **Băng Sát** | Thủy | Trực tiếp tức thời | **Làm chậm (Freeze/Slow)** | Kháng Băng (`ColdRes`) |
| **Lôi Sát** | Thổ | Trực tiếp tức thời | **Gây choáng (Stun)** | Kháng Lôi (`LightingRes`) |
| **Hỏa Sát** | Hỏa | Trực tiếp tức thời | **Gây bỏng / Đẩy lùi** | Kháng Hỏa (`FireRes`) |
| **Độc Sát** | Mộc | Rút máu theo thời gian (DoT)| **Trúng độc liên tục** | Kháng Độc (`PoisonRes`) |

---

## 2. Phân Biệt Sát Thương Ngoại Công vs Nội Công

### 2.1 Sát Thương Ngoại Công (Physical / Weapon-based Damage)
- **Cơ chế**: Dựa vào sức sát thương vật lý của **Vũ khí** đang cầm, điểm **Sức mạnh**, và chỉ số **% tăng sát thương** (`physicsenhance_p`).
- **Phụ thuộc**: Bắt buộc phải tính qua chỉ số **Chính xác (Attack Rating)** đối đầu với **Né tránh (Defense/Evasion)** của mục tiêu. Nếu trượt (`Miss`), đòn đánh không gây sát thương.
- **Tiêu biểu**: Thiên Vương Thương/Chùy, Thiếu Lâm Côn/Đao, Đường Môn Nỏ/Phi Đao, Võ Đang Kiếm, Thúy Yên Song Đao, Cái Bang Bổng.

### 2.2 Sát Thương Nội Công (Magical / Point-based Damage)
- **Cơ chế**: Sát thương được ghi dưới dạng điểm số cố định hoặc phạm vi min-max từ chính bảng kỹ năng (ví dụ: `colddamage_v = [200, 350]`, `firedamage_v = [500, 800]`).
- **Phụ thuộc**: Thường là sát thương diện rộng hoặc tia đạn bay, **luôn trúng mục tiêu khi va chạm**, không phụ thuộc vào né tránh của đối thủ.
- **Tiêu biểu**: Cái Bang Rồng (Phi Long Tại Thiên), Võ Đang Khí (Vô Ngã Vô Kiếm), Nga My Chưởng (Phong Sương Toái Ảnh), Thiên Nhẫn Ma Nhẫn (Thiên Ngoại Lưu Tinh), Côn Lôn Kiếm.

---

## 3. Chi Tiết Các Hiệu Ứng Trạng Thái Đi Kèm

### 3.1 Thọ Thương (Co Giật / Hit Recovery / Stagger)
- **Bản chất**: Khi nhân vật trúng một đòn sát thương vật lý vượt quá một tỷ lệ phần trăm nhất định so với lượng máu tối đa, cơ thể sẽ bị giật nảy về phía sau và rơi vào trạng thái `HurtFrame`.
- **Thông số Engine**: Trong [`Client_VLTK_SHXT/settings/npc/player/basevalue.ini`](../Client_VLTK_SHXT/settings/npc/player/basevalue.ini), thời gian co giật mặc định là:
  $$\text{HurtFrame} = 12 \text{ frames} \approx \frac{12}{18} \approx 0.67 \text{ giây}$$
- **Tác hại**: Trong suốt 12 frames này, nhân vật bị khựng lại, **không thể di chuyển, không thể bơm máu hay xuất chiêu**. Nếu bị nhiều kẻ địch đánh liên tục, nhân vật rơi vào trạng thái "khựng liên hoàn" (Stun-lock).
- **Cách khắc chế**: Thuộc tính **Thời gian phục hồi -%** (`hitrecover_reduce`) trên trang bị (giày, áo, dây chuyền) giúp giảm số frame co giật từ 12 xuống còn 5-6 frames.

---

### 3.2 Làm Chậm (Băng Sát - Freeze / Slow)
- **Bản chất**: Kích hoạt khi nhận sát thương Băng Sát từ phái hệ Thủy (Nga My, Thúy Yên).
- **Tác hại**:
  - Giảm tốc độ chạy (`RunSpeed`) từ 30% đến 60%.
  - **Giảm tốc độ xuất chiêu và tốc độ đánh** (`AttackSpeed`, `CastSpeed`), khiến động tác tấn công bị kéo dài hơn, xuất hiện độ trễ lớn.
- **Thời gian hiệu lực**: Tính theo frame (ví dụ: 54 frames = 3 giây).
- **Cách khắc chế**: Thuộc tính **Thời gian làm chậm -%** (`freezetimereduce_p`). Nếu đạt 100%, nhân vật hoàn toàn miễn nhiễm với hiệu ứng làm chậm của Băng sát!

---

### 3.3 Gây Choáng (Lôi Sát - Stun)
- **Bản chất**: Kích hoạt từ các đòn đánh Lôi Sát của phái hệ Thổ (Võ Đang, Côn Lôn) hoặc từ kỹ năng khống chế đặc biệt (Sư Tử Hống của Thiếu Lâm, Đoạn Hồn Thích của Thiên Vương).
- **Tác hại**:
  - Nhân vật bị **bất động 100%**: Không thể bước đi, không thể dùng kỹ năng, không thể sử dụng bình máu/mana trong hành trang.
  - Trên đầu nhân vật xuất hiện biểu tượng xoay tròn.
- **Cách khắc chế**: Thuộc tính **Thời gian làm choáng -%** (`stuntimereduce_p`) và **Kháng Lôi** cao để giảm tỷ lệ dính choáng.

---

### 3.4 Bỏng / Thiêu Đốt (Hỏa Sát - Burn)
- **Bản chất**: Xuất hiện khi trúng hỏa công từ Cái Bang hoặc Thiên Nhẫn.
- **Tác hại**:
  - Gây sát thương bộc phát tức thời cực lớn.
  - Một số kỹ năng hỏa sát đặc biệt (như Bổng Cái Bang) có thuộc tính **Đẩy lùi (Knockback)** ngắt quãng vị trí đối thủ.
- **Cách khắc chế**: Trang bị đồ có chỉ số **Kháng Hỏa** (`FireRes`) cao để triệt tiêu phần lớn lượng sát thương thiêu đốt.

---

### 3.5 Trúng Độc Rút Máu (Độc Sát - Poison / DoT)
- **Bản chất**: Độc sát là loại sát thương đặc biệt nhất trong VLTK:
  - **Không trừ máu ngay lập tức**, mà phân bổ đều thành các đợt rút máu nhỏ (**Ticks**) qua từng chu kỳ thời gian (mỗi tick cách nhau vài frames).
  - **Bỏ qua Né tránh**: Một khi đã trúng độc, máu chắc chắn sẽ tụt đều đặn.
  - **Không cho đối thủ ngồi thiền**: Duy trì trạng thái chiến đấu liên tục, khiến mục tiêu không thể bấm `V` để ngồi nghỉ hồi máu.
  - **Cơ chế bộc phát Độc**: Chiêu *Vạn Cổ Xuyên Tâm* của Ngũ Độc khiến toàn bộ lượng độc đang ngấm trong cơ thể phát tác dồn dập trong 1 giây, gây tử vong chớp nhoáng.
- **Cách khắc chế**: Thuộc tính **Thời gian trúng độc -%** (`poisontimereduce_p`) giúp rút ngắn thời gian độc tồn tại trong cơ thể, và chỉ số **Kháng Độc** (`PoisonRes`) để giảm lượng máu mất trong mỗi tick.

---

## 4. Công Thức Tính Sát Thương Thực Nhận

Khi mục tiêu nhận một đòn đánh nguyên tố (Băng, Lôi, Hỏa, Độc, Vật Lý), công thức tính sát thương thực tế vào máu là:

$$\text{Sát Thương Nhận} = \text{Sát Thương Gốc} \times \left(1 - \frac{\text{Kháng Tính \%}}{100}\right) \times \text{Hệ Số Ngũ Hành Tương Khắc}$$

- **Hệ số Khắc Hệ**:
  - Nếu người tấn công khắc hệ nạn nhân: Nhân thêm **$1.2 \rightarrow 1.4$** (+20% đến +40%).
  - Nếu người tấn công bị nạn nhân khắc hệ: Nhân thêm **$0.6 \rightarrow 0.8$** (-20% đến -40%).
- **Ngưỡng Trần Kháng Tính (Max Resist Cap)**:
  - Giá trị trần mặc định của các loại kháng là **75%**.
  - Các trang bị hoặc kỹ năng có thuộc tính "Kháng tối đa +%" có thể đẩy trần này lên mức **85% - 90%**, giúp giảm thiểu tối đa sát thương gánh chịu.
