# Công Thức Tính Lực Tay & Code Mô Phỏng (Damage Calculation & Code)

Tài liệu này trình bày chi tiết công thức toán học tính **Lực tay (Damage)** hiển thị trên bảng thuộc tính nhân vật (phím `F3`), phân biệt giữa **Chiêu thức Ngoại công** và **Chiêu thức Nội công**, cùng code Python tham khảo mô phỏng chính xác thuật toán của game.

---

## 1. Cơ Chế Lực Tay Hiển Thị Trên F3

Trên bảng giao diện nhân vật `F3`, lực tay luôn được biểu diễn dưới dạng một khoảng giá trị:
$$\text{Lực tay} = [\text{Damage Min}] - [\text{Damage Max}]$$

Khoảng giá trị này xuất phát từ việc:
1. Bản thân **Vũ khí** có sát thương min và max (ví dụ: Đao Cấp 10 có sát thương $75 - 110$).
2. Các dòng thuộc tính trên trang bị và chiêu thức có khoảng biến thiên ngẫu nhiên (ví dụ: Băng sát $40 - 65$).

---

## 2. Công Thức Tính Sát Thương Ngoại Công (Physical Weapon Skills)

Áp dụng cho các phái cận chiến hoặc dùng ám khí: **Thiên Vương, Thiếu Lâm Đao/Côn, Đường Môn Phi Đao/Nỏ, Võ Đang Kiếm, Thúy Yên Song Đao, Cái Bang Bổng**.

### 2.1 Các Thành Phần Trong Công Thức
1. **$W_{min}, W_{max}$**: Sát thương vật lý cơ bản của vũ khí đang trang bị.
2. **$B_{min}, B_{max}$**: Sát thương vật lý cộng thêm từ các trang bị khác (nhẫn, dây chuyền, bao tay...).
3. **$P_{str}$**: Điểm Sức mạnh của nhân vật. Với các phái dùng Thân pháp như Đường Môn nỏ/tiêu, điểm Thân pháp sẽ thay thế điểm Sức mạnh.
4. **$S_{passive}$**: Tổng phần trăm tăng sát thương từ **kỹ năng bị động cơ bản** (ví dụ: Thiếu Lâm Đao Pháp cấp 20 tăng 120%).
5. **$S_{active}$**: Phần trăm tăng sát thương vật lý của **chiêu thức xuất trận** (`physicsenhance_p`, ví dụ Vô Tướng Trảm cấp 20 tăng 350%).
6. **$S_{zhen}$**: Phần trăm từ kỹ năng trấn phái cấp 60 (ví dụ Dịch Cân Kinh, Thiên Vương Chiến Ý).
7. **$E_{element}$**: Sát thương nguyên tố ngoại công đi kèm (Băng sát, Hỏa sát, Lôi sát, Độc sát được ép từ vũ khí hoặc trang sức).

### 2.2 Công Thức Toán Học Chuẩn
$$\text{Damage}_{\text{min}} = \left(W_{\text{min}} + B_{\text{min}}\right) \times \left(1 + \frac{P_{\text{str}}}{100}\right) \times \left(1 + \frac{S_{\text{passive}} + S_{\text{active}} + S_{\text{zhen}}}{100}\right) + E_{\text{element}}$$

$$\text{Damage}_{\text{max}} = \left(W_{\text{max}} + B_{\text{max}}\right) \times \left(1 + \frac{P_{\text{str}}}{100}\right) \times \left(1 + \frac{S_{\text{passive}} + S_{\text{active}} + S_{\text{zhen}}}{100}\right) + E_{\text{element}}$$

---

## 3. Công Thức Tính Sát Thương Nội Công (Magical Skills)

Áp dụng cho các phái dùng chưởng pháp và kiếm khí từ xa: **Cái Bang Rồng, Võ Đang Khí, Nga My Chưởng, Thiên Nhẫn Ma Nhẫn, Côn Lôn Kiếm, Ngũ Độc Chưởng**.

### 3.1 Đặc Trưng Cốt Lõi
- **Không phụ thuộc vào sát thương của Vũ Khí**: Dù bạn cầm kiếm trắng Cấp 1 hay vũ khí Cấp 10, sát thương chiêu thức nội công cơ bản vẫn giữ nguyên!
- Điểm sát thương gốc xuất phát từ cấu hình trong file [`Client_VLTK_SHXT/settings/skills.txt`](../Client_VLTK_SHXT/settings/skills.txt).

### 3.2 Công Thức Toán Học
$$\text{Damage}_{\text{nội công}} = \text{SkillBasePoints} \times \left(1 + \frac{\sum \text{Kỹ Năng Hỗ Trợ Tương Hỗ \%}}{100}\right) + \text{Điểm Nguyên Tố Trang Bị}$$

- **Hỗ Trợ Tương Hỗ (Skill Synergy)**: Mỗi điểm cộng vào chiêu thức cấp thấp sẽ tăng một lượng % nhất định cho chiêu 90 hoặc 120 (ví dụ: Mỗi cấp *Kiến Long Tại Điền* tăng 5% sát thương cho *Phi Long Tại Thiên*).

---

## 4. Mã Nguồn Python Mô Phỏng Tính Lực Tay Chuẩn

Đoạn mã sau mô phỏng chính xác logic tính lực tay của game, bạn có thể chạy thử trực tiếp:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Bộ mô phỏng tính Lực tay VLTK (Damage Calculator)
"""

def calculate_physical_damage(
    weapon_min: int,
    weapon_max: int,
    bonus_phys_min: int,
    bonus_phys_max: int,
    stat_point: int,          # Sức mạnh (hoặc Thân pháp với Đường Môn)
    passive_weapon_pct: float,# % từ skill cơ bản (e.g. 120% -> 120.0)
    active_skill_pct: float,  # % từ skill xuất chiêu (e.g. 350% -> 350.0)
    zhenpai_pct: float,       # % từ trấn phái (e.g. 80% -> 80.0)
    elemental_min: int = 0,   # Băng sát / Lôi sát / Hỏa sát min
    elemental_max: int = 0    # Băng sát / Lôi sát / Hỏa sát max
):
    """Tính lực tay Ngoại công hiển thị trên F3"""
    total_pct = (passive_weapon_pct + active_skill_pct + zhenpai_pct) / 100.0
    stat_mult = 1.0 + (stat_point / 100.0)
    
    base_min = weapon_min + bonus_phys_min
    base_max = weapon_max + bonus_phys_max
    
    dmg_min = int(base_min * stat_mult * (1.0 + total_pct)) + elemental_min
    dmg_max = int(base_max * stat_mult * (1.0 + total_pct)) + elemental_max
    
    return dmg_min, dmg_max


def calculate_magical_damage(
    skill_base_min: int,
    skill_base_max: int,
    synergy_bonus_pct: float, # % tổng từ các skill hỗ trợ tương hỗ
    zhenpai_magic_pct: float, # % tăng nội công từ trấn phái
    gear_elemental_min: int = 0,
    gear_elemental_max: int = 0
):
    """Tính lực tay Nội công hiển thị trên F3"""
    total_pct = (synergy_bonus_pct + zhenpai_magic_pct) / 100.0
    
    dmg_min = int(skill_base_min * (1.0 + total_pct)) + gear_elemental_min
    dmg_max = int(skill_base_max * (1.0 + total_pct)) + gear_elemental_max
    
    return dmg_min, dmg_max


# ==============================================================
# VÍ DỤ CHẠY THỬ NGHIỆM
# ==============================================================
if __name__ == '__main__':
    print("=== 1. THIẾU LÂM ĐAO (NGOẠI CÔNG) ===")
    # Đao Cấp 10: 80 - 125 STVL
    # Sức mạnh: 260
    # Đao pháp: +120%, Vô Tướng Trảm: +380%, Dịch Cân Kinh: +90%
    # Băng sát từ nhẫn/vũ khí: 45 - 65
    d_min, d_max = calculate_physical_damage(
        weapon_min=80, weapon_max=125,
        bonus_phys_min=15, bonus_phys_max=25,
        stat_point=260,
        passive_weapon_pct=120.0,
        active_skill_pct=380.0,
        zhenpai_pct=90.0,
        elemental_min=45, elemental_max=65
    )
    print(f"Lực tay F3 Vô Tướng Trảm: {d_min} - {d_max}")

    print("\n=== 2. CÁI BANG CHƯỞNG (NỘI CÔNG) ===")
    # Phi Long Tại Thiên cấp 20: Hỏa sát gốc 650 - 920
    # Hỗ trợ từ Kiến Long + Thời Thừa: +180%
    # Hóa Cảnh Vô Vi (trấn phái): +60%
    m_min, m_max = calculate_magical_damage(
        skill_base_min=650, skill_base_max=920,
        synergy_bonus_pct=180.0,
        zhenpai_magic_pct=60.0
    )
    print(f"Lực tay F3 Phi Long Tại Thiên: {m_min} - {m_max} (Sát thương mỗi con rồng)")
```
