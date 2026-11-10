# Điểm Tiềm Năng & Tỷ Lệ Tăng Trưởng Hệ Phái (Potential Points & Growth)

Tài liệu này phân tích chi tiết tác động của **4 thuộc tính tiềm năng** (Sức mạnh, Thân pháp, Sinh khí, Nội công) lên các thông số của nhân vật, cùng bảng hệ số tăng trưởng thực tế được trích xuất từ tệp gốc [`Client_VLTK_SHXT/settings/npc/player/level_add.txt`](../Client_VLTK_SHXT/settings/npc/player/level_add.txt).

---

## 1. 4 Điểm Tiềm Năng Cơ Bản

Mỗi khi nhân vật lên cấp, người chơi nhận được **5 điểm tiềm năng** để tự do phân phối vào 4 nhánh:

| Thuộc Tính Tiềm Năng | Tên Kỹ Thuật | Tác Động Trực Tiếp Lên Nhân Vật |
| :--- | :---: | :--- |
| **Sức Mạnh** | `Strength` | Tăng sát thương vật lý ngoại công (Lực tay), đáp ứng điều kiện sức mạnh để cầm vũ khí nặng và mặc áo giáp nặng. |
| **Thân Pháp** | `Dexterity` | Tăng **Độ chính xác (Attack Rating)**, tăng **Né tránh (Defense/Evasion)**, tăng sát thương ngoại công cho phái dùng ám khí (Đường Môn). |
| **Sinh Khí** | `Vitality` | Tăng **Sinh lực tối đa (Máu / Max HP)**, tăng Thể lực tối đa (Stamina). |
| **Nội Công** | `Energy` | Tăng **Nội lực tối đa (Mana / Max MP)**, tăng sát thương cho một số chiêu thức nội công đặc thù. |

---

## 2. Bảng Tỷ Lệ Tăng Trưởng Máu & Mana Của 5 Hệ

Điểm đặc sắc nhất trong thiết kế cân bằng game của Kingsoft là **mỗi hệ ngũ hành có một hệ số nhân Máu và Mana hoàn toàn khác nhau**:

| Hệ Ngũ Hành | Môn Phái Tiêu Biểu | 1 Điểm Sinh Khí Tăng Bao Nhiêu Máu? | 1 Điểm Nội Công Tăng Bao Nhiêu Mana? | Tăng Máu Mỗi Cấp (`LifePerLevel`) | Tăng Mana Mỗi Cấp (`ManaPerLevel`) |
| :---: | :--- | :---: | :---: | :---: | :---: |
| **Hệ KIM** | **Thiếu Lâm, Thiên Vương** | **+8 HP (Cao nhất game!)** | +1 MP | +4 HP | +1 MP |
| **Hệ MỘC** | **Đường Môn, Ngũ Độc** | +5 HP | +3 MP | +3 HP | +2 MP |
| **Hệ THỦY** | **Nga My, Thúy Yên** | +6 HP | +3 MP | +3 HP | +2 MP |
| **Hệ HỎA** | **Cái Bang, Thiên Nhẫn** | **+7 HP** | +2 MP | +3 HP | +1 MP |
| **Hệ THỔ** | **Võ Đang, Côn Lôn** | +3 HP (Thấp nhất game) | **+4 MP (Cao nhất game!)** | +1 HP | +3 MP |

---

## 3. Phân Tích Chiến Lược Tăng Điểm Của Các Phái

### 3.1 Hệ KIM (Thiếu Lâm, Thiên Vương Bang) - "Xe Bọc Thép"
- **Đặc trưng**: Với hệ số khổng lồ **1 Sinh khí = 8 Máu**, các chiến binh hệ Kim có lượng máu tự nhiên cao nhất toàn cõi võ lâm.
- **Cách tăng điểm chuẩn**:
  - Tăng Sức mạnh vừa đủ để cầm vũ khí Cấp 10 (thường khoảng 260 - 300 điểm).
  - Tăng Thân pháp vừa đủ để đạt độ chính xác cần thiết khi PK.
  - **Dồn toàn bộ điểm còn lại vào Sinh khí** để biến thành một cỗ xe tăng bất tử với lượng máu 8.000 - 12.000+ HP!

### 3.2 Hệ THỔ (Võ Đang, Côn Lôn) - "Trường Phái Mana Hộ Thể"
- **Đặc trưng**: Hệ số sinh khí cực kỳ thấp (**1 Sinh khí chỉ được 3 Máu**). Nếu tăng Sinh khí, Võ Đang rất yếu ớt. Tuy nhiên, **1 Nội công lại đổi được tận 4 Mana**.
- **Cách tăng điểm chuẩn của Võ Đang Khí**:
  - Không tăng Sinh khí (hoặc chỉ tăng rất ít).
  - Bật chiêu thức trấn phái **Tọa Vọng Vô Vi** (`zuowang_wuwei`): Khiến 70% - 90% sát thương nhận vào bị trừ thẳng vào thanh Mana thay vì trừ vào Máu.
  - **Dồn tối đa điểm vào Nội Công** để có bình Mana 6.000 - 9.000+ MP. Khi Mana còn, Võ Đang hầu như không thể bị sốc sát thương chết!

### 3.3 Hệ MỘC (Đường Môn) - "Thân Pháp Chí Mạng"
- **Đặc trưng**: Đường Môn là môn phái duy nhất mà **Thân pháp vừa tăng Né tránh, vừa tăng Lực tay trực tiếp cho Bạo Vũ Lê Hoa và Cửu Cung Phi Tinh**.
- **Cách tăng điểm chuẩn**:
  - Tăng Sức mạnh vừa đủ mặc đồ (110 - 165 điểm).
  - **Dồn tối đa điểm vào Thân pháp** (350 - 500+ điểm) để tối ưu hóa sát thương nỏ/tiêu và đạt độ né tránh cực cao.
  - Phần còn lại đưa vào Sinh khí để tránh bị dính sát thương chết sốc.

### 3.4 Hệ HỎA (Cái Bang) & Hệ THỦY (Nga My)
- **Cái Bang**: Sở hữu hệ số máu tốt (+7 HP/Vit) và né tránh cao bẩm sinh từ chiêu Hóa Cảnh Vô Vi. Thường nâng Sức mạnh đủ mặc đồ, sau đó chia đều giữa Sinh khí và Thân pháp (đối với Bổng) hoặc Sinh khí và Nội công (đối với Rồng).
- **Nga My**: Cân bằng hài hòa giữa Máu (+6 HP) và Mana (+3 MP). Thường tăng Sinh khí cao để trụ vững hồi máu và hỗ trợ đồng đội trong hỗn chiến Tống Kim.
