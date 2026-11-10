# Thuộc Tính Trang Bị & Tác Động Lên Chỉ Số Nhân Vật (Equipment Attributes & Stats)

Tài liệu này hệ thống hóa toàn bộ **10 vị trí trang bị**, các phân cấp vật phẩm (Đồ Trắng, Đồ Xanh, Đồ Tím, Đồ Hoàng Kim) và danh mục các **thuộc tính ma pháp** cùng tác động trực tiếp lên bảng chỉ số của nhân vật.

---

## 1. 10 Vị Trí Trang Bị Trên Người Nhân Vật

Giao diện trang bị của nhân vật (`F4`) được chia làm 10 ô đồ theo sơ đồ chuẩn:

```text
       [  MŨ / ĐẦU  ]            [ DÂY CHUYỀN ]
       [   ÁO GIÁP   ]            [  ĐAI LƯNG  ]
       [   VŨ KHÍ   ]            [  GIÀY DÉP  ]
    [ NHẪN TRÊN / TRÁI ]      [ NHẪN DƯỚI / PHẢI ]
       [  BAO TAY   ]            [  NGỌC BỘI  ]
```

| STT | Vị Trí Trang Bị | Mã Tệp Cấu Hình | Thuộc Tính Đặc Trưng Nhất |
| :---: | :--- | :--- | :--- |
| 1 | **Vũ Khí** | `meleeweapon.txt` / `rangeweapon.txt` | Sát thương vật lý cơ bản, Tốc độ đánh, Băng sát, Hút máu/mana. |
| 2 | **Áo Giáp** | `armor.txt` | Phòng thủ vật lý cơ bản, Sinh lực tối đa, Kháng tất cả, Giảm thọ thương. |
| 3 | **Mũ Trụ** | `helm.txt` | Phòng thủ, Phục hồi sinh lực/nội lực, Kháng ngũ hành. |
| 4 | **Dây Chuyền** | `necklace.txt` | Tốc độ xuất chiêu, Kháng ngũ hành, Kỹ năng vốn có +1, Tỷ lệ né tránh. |
| 5 | **Đai Lưng** | `belt.txt` | Sinh lực tối đa, Kháng ngũ hành, Thời gian làm chậm/choáng -%. |
| 6 | **Giày** | `boot.txt` | **Tốc độ di chuyển +% (quan trọng nhất)**, Thời gian phục hồi -%. |
| 7 | **Nhẫn Trên** | `ring.txt` | Sát thương nguyên tố, Sát thương vật lý điểm, Kháng ngũ hành, May mắn. |
| 8 | **Nhẫn Dưới** | `ring.txt` | Tương tự nhẫn trên, hỗ trợ kích hoạt ngũ hành. |
| 9 | **Bao Tay** | `cuff.txt` | **Tốc độ đánh +%**, Độ chính xác, Hút sinh lực, Kháng ngũ hành. |
| 10 | **Ngọc Bội** | `pendant.txt` | Kháng tính, Né tránh, Thời gian trúng độc/làm chậm -%. |

---

## 2. Phân Loại Phẩm Cấp Trang Bị

1. **Đồ Trắng (Normal Items)**:
   - Chỉ có thuộc tính vật lý cơ bản (sát thương min-max của vũ khí, phòng thủ của áo mũ).
   - Không có dòng ma pháp phụ trợ nào.
2. **Đồ Xanh (Magic Items)**:
   - Có từ 1 đến 6 dòng thuộc tính ma pháp.
   - **Cơ chế 3 Dòng Hiện & 3 Dòng Ẩn**:
     - 3 dòng hiện có hiệu lực ngay lập tức khi mặc.
     - 3 dòng ẩn chỉ sáng lên khi được kích hoạt bởi trang bị có ngũ hành tương sinh tương ứng.
3. **Đồ Tím / Đồ Bộ (Set Items - An Bang, Định Quốc)**:
   - Các bộ trang sức và phòng cụ định danh huyền thoại.
   - Khi mặc đủ 2 món, 3 món hoặc trọn bộ 4 món sẽ kích hoạt thêm các dòng siêu phẩm (Kháng tất cả +20%, Kỹ năng +1, Sinh lực +500).
4. **Đồ Hoàng Kim Môn Phái (Golden Sect Items)**:
   - Trang bị tối thượng mang tên các vị chưởng môn / huyền thoại (Ỷ Thiên Kiếm, Đả Cẩu Bổng, Hám Thiên Chùy, Băng Hàn Thúy Yên Đao...).
   - Sở hữu các dòng độc tôn: Kỹ năng môn phái +2, Tốc độ đánh 30-40%, Hút hít cực cao.

---

## 3. Bảng Tra Cứu Toàn Diện Các Thuộc Tính Ma Pháp (`magicdesc.ini`)

### 3.1 Nhóm Sinh Tồn: Máu, Mana & Phục Hồi
- `lifemax_v` / `lifemax_p`: Tăng **Sinh lực tối đa** theo điểm cố định (ví dụ: +150 Máu) hoặc theo phần trăm (+15%).
- `manamax_v` / `manamax_p`: Tăng **Nội lực tối đa** theo điểm (+120 Mana) hoặc phần trăm.
- `staminamax_v`: Tăng Thể lực tối đa (giúp chạy bộ bền bỉ hơn không bị tụt thể lực).
- `lifereplenish_v`: **Phục hồi sinh lực** mỗi giây (giúp hồi máu tự nhiên mà không cần cắn bình).
- `manareplenish_v`: **Phục hồi nội lực** mỗi giây.

### 3.2 Nhóm Hút Sinh Lực & Nội Lực (Lifesteal & Manasteal)
- `steallife_p`: **Hút sinh lực khi đánh trúng**: Chuyển một phần trăm sát thương gây ra trực tiếp thành máu cho bản thân (ví dụ: Hút 5% sinh lực). Cực kỳ thiết yếu cho các phái cận chiến cày cấp và săn boss.
- `stealmana_p`: **Hút nội lực khi đánh trúng**: Đánh trúng đối thủ sẽ hồi mana lập tức, giúp xuất chiêu liên tục không sợ cạn bình mana.

### 3.3 Nhóm Kháng Ngũ Hành (Elemental Resistances)
- `fireres_p`: **Kháng Hỏa** (giảm sát thương của Cái Bang, Thiên Nhẫn).
- `coldres_p`: **Kháng Băng** (giảm sát thương của Nga My, Thúy Yên).
- `lightingres_p`: **Kháng Lôi** (giảm sát thương của Võ Đang, Côn Lôn).
- `poisonres_p`: **Kháng Độc** (giảm lượng máu mất khi trúng độc của Ngũ Độc, Đường Môn).
- `physicsres_p`: **Kháng Vật Lý** (giảm sát thương ngoại công của mọi vũ khí chém/đâm/đập).
- `allres_p`: **Kháng tất cả** (tăng đồng thời cả 5 loại kháng).
- `allresmax_p`: **Kháng tối đa +%** (nâng ngưỡng trần kháng từ 75% lên 80-85%).

### 3.4 Nhóm Kháng Hiệu Ứng Khống Chế (Control Reduction)
- `freezetimereduce_p`: **Thời gian làm chậm -%** (mặc định 100% là miễn nhiễm làm chậm).
- `stuntimereduce_p`: **Thời gian làm choáng -%** (giảm số giây bất động khi bị giật sét).
- `poisontimereduce_p`: **Thời gian trúng độc -%** (khiến độc tan nhanh chóng trong cơ thể).
- `hitrecover_reduce`: **Thời gian phục hồi -%** (giảm số frame co giật khi bị thọ thương, giúp nhân vật hồi tỉnh và tiếp tục hành động ngay).

### 3.5 Nhóm Tốc Độ & Công Kích
- `fastwalkrun_p`: **Tốc độ di chuyển +%** (xuất hiện độc quyền trên Giày dép, từ 20% đến 40%).
- `attackspeed_p`: **Tốc độ đánh ngoại công +%** (trên Vũ khí và Bao tay).
- `castspeed_p`: **Tốc độ xuất chiêu nội công +%** (trên Dây chuyền và Vũ khí).
- `attackrating_v` / `attackrating_p`: **Độ chính xác** (tăng tỷ lệ đánh trúng mục tiêu né cao).
- `armordefense_v` / `armordefense_p`: **Né tránh** (tăng tỷ lệ khiến đòn đánh ngoại công của đối thủ thành `Miss`).
- `deadlystrike_p`: **Xác suất xuất chiêu chí mạng / Đòn chí mạng +%** (nhân đôi sát thương).

---

## 4. Cơ Chế Kích Hoạt Dòng Ẩn Bằng Ngũ Hành (Equip Activation Chain)

Để một món Đồ Xanh sáng trọn vẹn cả 3 dòng ẩn, người chơi phải trang bị món đồ khác có hành **Sinh** ra nó ở các vị trí tương hỗ theo chuỗi:

$$\text{Mũ (Head)} \rightarrow \text{Áo (Body)} \rightarrow \text{Đai Lưng (Belt)} \rightarrow \text{Giày (Boot)} \rightarrow \text{Bao Tay (Cuff)}$$
$$\text{Dây Chuyền} \rightarrow \text{Ngọc Bội} \rightarrow \text{Nhẫn Trên} \rightarrow \text{Nhẫn Dưới} \rightarrow \text{Vũ Khí}$$

- **Ví dụ**:
  - Bạn có một thanh Kiếm hệ **Thủy** có dòng ẩn 1: Băng sát +60 điểm, dòng ẩn 2: Tốc đánh +20%.
  - Để 2 dòng này sáng lên, bạn cần đeo **Nhẫn Dưới hệ KIM** (vì Kim sinh Thủy).
  - Khi Nhẫn Kim được trang bị, thanh Kiếm Thủy lập tức kích hoạt toàn bộ sức mạnh ẩn giấu!
