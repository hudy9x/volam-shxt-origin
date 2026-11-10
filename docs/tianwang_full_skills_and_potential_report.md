# Báo Cáo Kỹ Thuật: Toàn Bộ Kỹ Năng (Level 10 - 150) & Công Thức Điểm Tiềm Năng Thiên Vương Bang

> **Mục đích tài liệu**: Tài liệu này đóng vai trò là chuẩn tham chiếu (Ground Truth Reference) được trích xuất trực tiếp từ mã nguồn cấu hình client game (`Client_VLTK_SHXT/settings/skills.txt`, `Client_VLTK_SHXT/script/skill/tianwang.lua`, và `Client_VLTK_SHXT/settings/npc/player/level_add.txt`). Tài liệu dùng làm đầu vào độc lập để so sánh, đối soát và đối chiếu tính nhất quán với các codebase Võ Lâm Truyền Kỳ khác.

---

## 1. Công Thức & Cơ Chế Điểm Tiềm Năng Của Thiên Vương Bang (Hệ KIM)

Thiên Vương Bang thuộc **Hệ KIM**, là môn phái cận chiến ngoại công sở hữu lượng máu tự nhiên và hệ số sinh khí cao nhất trong ngũ hành.

### 1.1 Bảng Hệ Số Tăng Trưởng Gốc Hệ KIM (Trích xuất từ `level_add.txt`)

| Thuộc Tính Tiềm Năng | Mã Hệ Thống | Giá Trị Hệ Số Tăng Trưởng | Ý Nghĩa Kỹ Thuật |
| :--- | :--- | :---: | :--- |
| **Sinh Khí -> Máu** | `LifePerVitality` | **+8 HP** | **1 điểm Sinh Khí tăng 8 Máu** (Cao nhất ngũ hành, ngang Thiếu Lâm) |
| **Nội Công -> Mana** | `ManaPerEnergy` | **+1 MP** | 1 điểm Nội Công chỉ tăng 1 Mana (Thấp nhất ngũ hành) |
| **Máu Tăng Mỗi Cấp** | `LifePerLevel` | **+4 HP** | Mỗi khi nhân vật lên 1 level, tự động tăng 4 Máu |
| **Mana Tăng Mỗi Cấp** | `ManaPerLevel` | **+1 MP** | Mỗi khi nhân vật lên 1 level, tự động tăng 1 Mana |
| **Thể Lực (Nam) / Cấp** | `StaminaMalePerLevel` | **+9 Thể lực** | Gia tăng thể lực phục vụ chạy bộ và khinh công |
| **Thể Lực Cơ Bản** | `StaminaMaleBase` | **180** | Điểm thể lực khởi tạo ban đầu |
| **Sức Mạnh -> Lực Tay** | `Strength` | Tăng (1 + SM/100) | Hệ số nhân trực tiếp vào sát thương vật lý ngoại công |
| **Thân Pháp -> Chính Xác & Né** | `Dexterity` | Tăng AR & Defense | Tăng độ chính xác đánh trúng và né tránh ngoại công |

### 1.2 Kháng Tính Tự Nhiên Ban Đầu (Hệ KIM)
- **Kháng Độc (`poisonres`)**: **+25%** *(Kim khắc Mộc - Thiên Vương bẩm sinh kháng độc tự nhiên)*.
- **Kháng Hỏa (`fireres`)**: **-25%** *(Hỏa khắc Kim - Thiên Vương bẩm sinh sợ hỏa công của Cái Bang/Thiên Nhẫn)*.
- **Kháng Băng (`coldres`)**: **0%**.
- **Kháng Lôi (`lightingres`)**: **0%**.
- **Kháng Vật Lý (`physicres`)**: **0%**.

### 1.3 Thông Số Khung Hình Cơ Bản (Trích xuất từ `basevalue.ini`)
- Thời gian thọ thương co giật khi trúng đòn: `HurtFrame = 12 frames` (khoảng 0.67 giây).
- Tốc độ chạy cơ bản: `RunSpeed = 10`.
- Tốc độ đi bộ cơ bản: `WalkSpeed = 5`.
- Tốc độ xuất chiêu / tấn công chuẩn: `AttackFrame = 18`, `CastFrame = 18`.

### 1.4 Công Thức Toán Học Tính Máu & Mana Của Thiên Vương Bang

$$\text{Máu Cơ Bản} = (\text{Level} \times 4) + (\text{Điểm Sinh Khí} \times 8) + \text{Máu Từ Trang Bị}$$

$$\text{Máu Thực Tế Khi Bật Chiến Ý} = \text{Máu Cơ Bản} \times \left(1 + \frac{\text{% Máu Từ Thiên Vương Chiến Ý}}{100}\right)$$

*(Ở Cấp 30 Chiến Ý, lượng máu được nhân thêm tới +185%, tức gấp gần 3 lần lượng máu cơ bản!)*

---

## 2. Bảng Tra Cứu Toàn Diện 23 Kỹ Năng Thiên Vương (Level 10 - 150)

| STT | Kỹ Năng | Tên Hán Tự | Mã Script | Skill ID | Cấp Y/C | Nhánh Võ Công | Dạng Kỹ Năng |
| :-: | :--- | :--- | :--- | :-: | :-: | :--- | :--- |
| 1 | **Thiên Vương Thương Pháp** | 天王枪法 | `tianwang_qiangfa` | 23 | Cấp 10 | Thương | Bị |
| 2 | **Dương Gia Thương Pháp / Hành Vân Quyết** | 行云诀 | `xingyun_jue` | 31 | Cấp 30 | Thương | Chủ |
| 3 | **Vô Tâm Trảm** | 无心斩 | `wuxin_zhan` | 32 | Cấp 60 | Thương | Chủ |
| 4 | **Huyết Chiến Bát Phương** | 血战八方 | `xuezhan_bafang` | 41 | Cấp 90 | Thương | Chủ |
| 5 | **Thừa Long Quyết** | 乘龙诀 | `chenglong_jue` | 324 | Cấp 120 | Thương | Chủ |
| 6 | **Bá Vương Tán Kim** | 枪天150 / 霸王錾金 | `qiangtianwang150` | 1060 | Cấp 150 | Thương | Chủ |
| 7 | **Thiên Vương Chùy Pháp** | 天王锤法 | `tianwang_chuifa` | 26 | Cấp 10 | Chùy | Bị |
| 8 | **Trảm Long Quyết** | 斩龙诀 | `zhanlong_jue` | 29 | Cấp 30 | Chùy | Chủ |
| 9 | **Dương Quan Tam Điệp** | 阳关三叠 | `yangguan_sandie` | 35 | Cấp 60 | Chùy | Chủ |
| 10 | **Hồi Phong Lạc Nhạn** | 回风落雁 | `huifeng_luoyan` | 30 | Cấp 30 | Chùy | Chủ |
| 11 | **Truy Tinh Trục Nguyệt** | 追星逐月 | `zhuixing_zhuyue` | 323 | Cấp 90 | Chùy | Chủ |
| 12 | **Truy Phong Quyết** | 追风诀 | `zhuifeng_jue` | 325 | Cấp 120 | Chùy | Chủ |
| 13 | **Tung Hoành Bát Hoang** | 锤天王150 / 纵横八荒 | `chuitianwang150` | 1059 | Cấp 150 | Chùy | Chủ |
| 14 | **Thiên Vương Đao Pháp** | 天王刀法 | `tianwang_daofa` | 24 | Cấp 10 | Đao | Bị |
| 15 | **Kinh Lôi Trảm** | 惊雷斩 | `jinglei_zhan` | 34 | Cấp 30 | Đao | Chủ |
| 16 | **Phách Phong Trảm** | 泼风斩 | `pofeng_zhan` | 37 | Cấp 60 | Đao | Chủ |
| 17 | **Phá Thiên Trảm** | 破天斩 | `potian_zhan` | 322 | Cấp 90 | Đao | Chủ |
| 18 | **Đảo Hư Thiên** | 倒虚天 | `daoxutian` | 708 | Cấp 120 | Đao | Chủ |
| 19 | **Hào Hùng Trảm** | 刀天150 / 豪雄斩 | `daotianwang150` | 1058 | Cấp 150 | Đao | Chủ |
| 20 | **Tĩnh Tâm Quyết** | 静心诀 | `jingxin_jue` | 33 | Cấp 20 | Bổ | Bị |
| 21 | **Đoạn Hồn Thích** | 断魂刺 | `duanhun_ci` | 40 | Cấp 40 | Kỹ | Chủ |
| 22 | **Kim Chung Trạo** | 金钟罩 | `jinzhong_zhao` | 42 | Cấp 50 | Bổ | Chủ |
| 23 | **Thiên Vương Chiến Ý** | 天王战意 | `tianwang_zhanyi` | 36 | Cấp 60 | Kỹ | Bị |

---

## 3. Đặc Tả Thuộc Tính Ma Pháp Chi Tiết Từng Kỹ Năng (23 Skills Specification)

> [!NOTE]
> Cấu trúc dữ liệu nội suy trong `tianwang.lua` được quy ước theo dạng:
> `{{{1, Val_L1}, {20, Val_L20}, {Max, Val_LMax}}, {{1, Param2_L1}, ...}}`
> Trong đó giá trị ở các level trung gian được nội suy tuyến tính giữa các điểm mốc.

### 3.1 [23] Thiên Vương Thương Pháp (天王枪法)
- **Mã kỹ thuật (Script key)**: `tianwang_qiangfa`
- **Skill ID**: `23` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng thương pháp cơ bản môn phái. Tăng vĩnh viễn sát thương vật lý vũ khí, độ chính xác và xác suất ra đòn chí mạng khi sử dụng Thương.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,25},{20,315}},{{1,-1},{2,-1}},{{1,3},{2,3}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,75},{20,270}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.2 [31] Dương Gia Thương Pháp / Hành Vân Quyết (行云诀)
- **Mã kỹ thuật (Script key)**: `xingyun_jue`
- **Skill ID**: `31` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `30` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Chiêu đâm thương kèm sát thương Băng sát và hiệu ứng bỏ qua né tránh/phòng thủ của mục tiêu.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,30},{20,255}}}` |
| `ignoredefense_p` | ignoredefense_p | `{{{1,10},{20,35}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,5},{20,30}}}` |
| `colddamage_v` | colddamage_v | `{` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,8},{20,20}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,22},{20,22}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,66},{20,66}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,3},{20,7}}}` |

### 3.3 [32] Vô Tâm Trảm (无心斩)
- **Mã kỹ thuật (Script key)**: `wuxin_zhan`
- **Skill ID**: `32` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `60` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng xuất chiêu uy lực cao, đồng thời hỗ trợ tăng thêm sát thương tương hỗ cho Phá Thiên Trảm (+80%) và Hào Hùng Trảm (+67%).

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,65},{20,453}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,10},{20,50},{21,52}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,4},{20,25}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `addskilldamage5` | addskilldamage5 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,26},{20,26}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,78},{20,78}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{20,20}}}` |

### 3.4 [41] Huyết Chiến Bát Phương (血战八方)
- **Mã kỹ thuật (Script key)**: `xuezhan_bafang`
- **Skill ID**: `41` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Chủ động tấn công (Active - Cấp 90)`
- **Cấp độ yêu cầu**: Level `90` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tuyệt kỹ trấn phái nhánh Thương cấp 90. Đâm ra 5 thức thương liên hoàn chớp nhoáng với tốc độ cực cao, dồn ép đối thủ vào trạng thái thọ thương liên tục.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,60},{20,723}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,10},{20,50},{21,52}}}` |
| `attackrating_p` | attackrating_p | `{{{1,75},{20,320}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,4},{20,25}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,26},{20,26}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,78},{20,78}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,11},{20,45}}}` |

### 3.5 [324] Thừa Long Quyết (乘龙诀)
- **Mã kỹ thuật (Script key)**: `chenglong_jue`
- **Skill ID**: `324` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Chủ động tấn công (Active - Cấp 120)`
- **Cấp độ yêu cầu**: Level `120` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng đại thừa Cấp 120 nhánh Thương. Tăng cường sát thương xuyên phá và đẩy tỉ lệ chí mạng lên mức 40%.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,40},{20,495}}}` |
| `ignoredefense_p` | ignoredefense_p | `{{{1,38},{20,80},{21,82}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,10},{20,50},{21,52}}}` |
| `colddamage_v` | colddamage_v | `{` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,5},{20,40}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,26},{20,26}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,78},{20,78}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{20,16}}}` |

### 3.6 [1060] Bá Vương Tán Kim (枪天150 / 霸王錾金)
- **Mã kỹ thuật (Script key)**: `qiangtianwang150`
- **Skill ID**: `1060` | **Nhánh**: `Thương Pháp (Spear)` | **Loại**: `Chủ động tấn công (Active - Cấp 150)`
- **Cấp độ yêu cầu**: Level `150` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Bá Vương Chi Lực, Toái Kim Phá Thạch. Kỹ năng Cấp 150 đại thừa của Thiên Vương Thương, đâm xuyên mục tiêu từ 3 hướng trực diện diện rộng.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,35},{10,350},{20,700},{50,1750},{51,1750}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,40},{15,40},{20,80},{21,82}}}` |
| `attackrating_p` | attackrating_p | `{{{1,40},{20,800},{21,800},{26,800}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,6},{20,40},{23,48},{26,54}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,36},{20,36}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,5},{20,5}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,180},{20,180}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,12},{20,80},{23,101}}}` |
| `skill_eventskilllevel` | skill_eventskilllevel | `{{{1,1},{20,20}}}` |
| `skill_misslenum_v` | skill_misslenum_v | `{{{1,32},{5,32},{20,32},{21,32}}}` |
| `skill_startevent` | skill_startevent | `{` |

### 3.7 [26] Thiên Vương Chùy Pháp (天王锤法)
- **Mã kỹ thuật (Script key)**: `tianwang_chuifa`
- **Skill ID**: `26` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng chùy pháp cơ bản môn phái. Tăng vĩnh viễn sát thương vật lý vũ khí, độ chính xác và xác suất đòn chí mạng khi cầm Chùy.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,25},{20,275}},{{1,-1},{2,-1}},{{1,4},{2,4}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,15},{20,72}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.8 [29] Trảm Long Quyết (斩龙诀)
- **Mã kỹ thuật (Script key)**: `zhanlong_jue`
- **Skill ID**: `29` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `30` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Cú nện chùy dũng mãnh kèm hiệu ứng Băng sát làm chậm và bỏ qua phòng ngự của kẻ địch.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,80},{20,185}}}` |
| `ignoredefense_p` | ignoredefense_p | `{{{1,5},{20,20}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,1},{20,10}}}` |
| `colddamage_v` | colddamage_v | `{` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,6},{20,10}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `addskilldamage5` | addskilldamage5 | `{` |
| `addskilldamage6` | addskilldamage6 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,18},{20,18}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,54},{20,54}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,2},{20,6}}}` |

### 3.9 [35] Dương Quan Tam Điệp (阳关三叠)
- **Mã kỹ thuật (Script key)**: `yangguan_sandie`
- **Skill ID**: `35` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `60` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng chùy đập 3 đợt sóng xung kích uy dũng, hỗ trợ tăng thêm sát thương tương hỗ cho Truy Tinh Trục Nguyệt (+65%) và Tung Hoành Bát Hoang (+54%).

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,130},{20,375}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,5},{20,30}}}` |
| `attackrating_p` | attackrating_p | `{{{1,10},{20,180}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,22},{20,22}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,66},{20,66}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,9},{20,16}}}` |

### 3.10 [30] Hồi Phong Lạc Nhạn (回风落雁)
- **Mã kỹ thuật (Script key)**: `huifeng_luoyan`
- **Skill ID**: `30` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `30` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng xoay chùy hỗ trợ, tăng sát thương cho Truy Tinh Trục Nguyệt (+60%), Huyết Chiến Bát Phương (+15%) và Tung Hoành Bát Hoang (+50%).

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `seriesdamage_p` | seriesdamage_p | `{{{1,1},{20,10}}}` |
| `physicsenhance_p` | physicsenhance_p | `{{{1,80},{20,215}}}` |
| `attackrating_p` | attackrating_p | `{{{1,10},{20,147}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `addskilldamage5` | addskilldamage5 | `{` |
| `addskilldamage6` | addskilldamage6 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,18},{20,18}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,54},{20,54}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,4},{20,10}}}` |

### 3.11 [323] Truy Tinh Trục Nguyệt (追星逐月)
- **Mã kỹ thuật (Script key)**: `zhuixing_zhuyue`
- **Skill ID**: `323` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active - Cấp 90)`
- **Cấp độ yêu cầu**: Level `90` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tuyệt kỹ Chùy cấp 90 trời giáng. Một cú bổ nổ chùy sấm sét uy lực vô song, kèm tỉ lệ làm choáng và sát thương chí mạng cực cao khiến đối thủ bốc hơi tức thì.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,50},{15,200},{20,381}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,20},{15,20},{20,60},{21,62}}}` |
| `attackrating_p` | attackrating_p | `{{{1,95},{20,360}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,4},{20,25}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,30},{20,30}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,90},{20,90}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{20,65}}}` |
| `addskillexp1` | addskillexp1 | `{{{1,323},{2,323}},{{1,1},{20,1}},{{1,0},{2,0}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,SkillExpFunc(6550,1.25,1,5,1)}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |

### 3.12 [325] Truy Phong Quyết (追风诀)
- **Mã kỹ thuật (Script key)**: `zhuifeng_jue`
- **Skill ID**: `325` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active - Cấp 120)`
- **Cấp độ yêu cầu**: Level `120` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng đại thừa Cấp 120 nhánh Chùy, tăng cường tốc độ bổ chùy và đẩy tỉ lệ chí mạng lên +40%.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,25},{15,140},{20,380}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,20},{15,20},{20,60},{21,62}}}` |
| `ignoredefense_p` | ignoredefense_p | `{{{1,12},{20,90},{21,94},{22,98},{23,99},{24,99}}}` |
| `colddamage_v` | colddamage_v | `{` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,5},{20,40}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,30},{20,30}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,90},{20,90}}}` |
| `addskillexp1` | addskillexp1 | `{{{1,325},{2,325}},{{1,1},{20,1}},{{1,0},{2,0}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,SkillExpFunc(7750,1.25,1,2.5,1)}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{20,30}}}` |

### 3.13 [1059] Tung Hoành Bát Hoang (锤天王150 / 纵横八荒)
- **Mã kỹ thuật (Script key)**: `chuitianwang150`
- **Skill ID**: `1059` | **Nhánh**: `Chùy Pháp (Hammer)` | **Loại**: `Chủ động tấn công (Active - Cấp 150)`
- **Cấp độ yêu cầu**: Level `150` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng Chùy Cấp 150 tối thượng. Đập nổ xung chấn chùy ngút trời, tỉ lệ chí mạng tự thân lên tới 50% - 71%, dồn sát thương bạo liệt toàn màn hình.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,40},{15,360},{20,655},{23,979},{26,1156}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,40},{15,40},{20,80},{21,82}}}` |
| `ignoredefense_p` | ignoredefense_p | `{{{1,12},{20,90},{21,94},{22,98},{23,99},{24,99}}}` |
| `colddamage_v` | colddamage_v | `{` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,5},{20,50},{23,64},{26,71}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,36},{20,36}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,5},{20,5}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,180},{20,180}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,12},{20,36},{23,43}}}` |
| `skill_eventskilllevel` | skill_eventskilllevel | `{{{1,1},{20,20}}}` |
| `skill_misslenum_v` | skill_misslenum_v | `{{{1,32},{5,32},{20,32},{21,32}}}` |
| `skill_startevent` | skill_startevent | `{` |

### 3.14 [24] Thiên Vương Đao Pháp (天王刀法)
- **Mã kỹ thuật (Script key)**: `tianwang_daofa`
- **Skill ID**: `24` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng đao pháp cơ bản môn phái. Tăng vĩnh viễn 300% sát thương vật lý vũ khí, độ chính xác và 15% chí mạng khi dùng Đao.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,50},{20,300}},{{1,-1},{2,-1}},{{1,1},{2,1}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,15},{20,72}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.15 [34] Kinh Lôi Trảm (惊雷斩)
- **Mã kỹ thuật (Script key)**: `jinglei_zhan`
- **Skill ID**: `34` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `30` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Đao pháp sấm sét, đồng thời là chiêu thức hỗ trợ tương hỗ tăng 60% sát thương cho Phá Thiên Trảm và 50% cho Hào Hùng Trảm 150.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,40},{20,200}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,1},{20,10}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `addskilldamage5` | addskilldamage5 | `{` |
| `addskilldamage6` | addskilldamage6 | `{` |
| `addskilldamage7` | addskilldamage7 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,18},{20,18}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,54},{20,54}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,5},{20,10}}}` |

### 3.16 [37] Phách Phong Trảm (泼风斩)
- **Mã kỹ thuật (Script key)**: `pofeng_zhan`
- **Skill ID**: `37` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Chủ động tấn công (Active)`
- **Cấp độ yêu cầu**: Level `60` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Đao pháp gió lốc quét rộng, hỗ trợ tăng 70% sát thương cho Phá Thiên Trảm và 58% (cấp 27 là 98%) cho Hào Hùng Trảm 150.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,120},{20,275}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,5},{20,30}}}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |
| `addskilldamage4` | addskilldamage4 | `{` |
| `addskilldamage5` | addskilldamage5 | `{` |
| `missle_speed_v` | missle_speed_v | `{{{1,22},{20,22}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,66},{20,66}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,8},{20,12}}}` |

### 3.17 [322] Phá Thiên Trảm (破天斩)
- **Mã kỹ thuật (Script key)**: `potian_zhan`
- **Skill ID**: `322` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Chủ động tấn công (Active - Cấp 90)`
- **Cấp độ yêu cầu**: Level `90` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tuyệt kỹ Đao cấp 90. Vung đao khí hình cánh cung quét rộng, gây sát thương vật lý lớn và hỗ trợ thêm 35% sát thương cho Hào Hùng Trảm 150.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,35},{15,150},{20,338}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,20},{15,20},{20,60},{21,62}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,4},{20,25}}}` |
| `attackrating_p` | attackrating_p | `{{{1,35},{20,215}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,30},{20,30}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,4},{20,4}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,90},{20,90}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,15},{20,30}}}` |
| `addskillexp1` | addskillexp1 | `{{{1,322},{2,322}},{{1,1},{20,1}},{{1,0},{2,0}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,SkillExpFunc(7280,1.25,1,2.5,1)}` |
| `addskilldamage1` | addskilldamage1 | `{` |
| `addskilldamage2` | addskilldamage2 | `{` |
| `addskilldamage3` | addskilldamage3 | `{` |

### 3.18 [708] Đảo Hư Thiên (倒虚天)
- **Mã kỹ thuật (Script key)**: `daoxutian`
- **Skill ID**: `708` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Chủ động Hộ Thân (Buff - Cấp 120)`
- **Cấp độ yêu cầu**: Level `120` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tuyệt kỹ hộ thân tối thượng của Thiên Vương Đao. Tăng 10% tất cả kháng tính, tăng trần kháng tối đa +5%, tăng tốc độ hồi phục sinh lực +35% và bỏ qua hiệu ứng khống chế của đối thủ.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `allres_p` | allres_p | `{{{1,1},{20,10},{21,10}},{{1,-1},{2,-1}}}` |
| `allresmax_p` | allresmax_p | `{{{1,1},{20,5},{21,5}},{{1,-1},{2,-1}}}` |
| `lifereplenish_p` | lifereplenish_p | `{{{1,1},{20,35},{28,50},{29,50}},{{1,-1},{2,-1}}}` |
| `ignoreskill_p` | ignoreskill_p | `{{{1,1},{28,100},{29,100}},{{1,-1},{2,-1}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,17851239}` |

### 3.19 [1058] Hào Hùng Trảm (刀天150 / 豪雄斩)
- **Mã kỹ thuật (Script key)**: `daotianwang150`
- **Skill ID**: `1058` | **Nhánh**: `Đao Pháp (Blade)` | **Loại**: `Chủ động tấn công (Active - Cấp 150)`
- **Cấp độ yêu cầu**: Level `150` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng Đao Cấp 150 đại thừa. Phóng thích đao khí cuồn cuộn tỏa rộng toàn diện, sức công phá vũ bão khi kết hợp đầy đủ 4 tầng hỗ trợ tương hỗ.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,30},{10,300},{40,1200},{50,1500},{51,1500}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,40},{15,40},{20,80},{21,82}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,5},{20,30},{23,37},{26,41}}}` |
| `attackrating_p` | attackrating_p | `{{{1,20},{30,600},{31,600}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,36},{20,36}}}` |
| `missle_lifetime_v` | missle_lifetime_v | `{{{1,14},{20,14}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,480},{20,480}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,20},{20,35},{23,39}}}` |
| `skill_eventskilllevel` | skill_eventskilllevel | `{{{1,1},{20,20}}}` |
| `skill_misslenum_v` | skill_misslenum_v | `{{{1,32},{5,32},{20,32},{21,32}}}` |
| `skill_collideevent` | skill_collideevent | `{` |
| `skill_showevent` | skill_showevent | `{{{1,0},{10,0},{10,5},{20,5}}}` |
| `addskillexp1` | addskillexp1 | `{{{1,1058},{2,1058}},{{1,1},{20,1}},{{1,0},{2,0}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,SkillExpFunc(7280,1.25,1,2.5,1)}` |

### 3.20 [33] Tĩnh Tâm Quyết (静心诀)
- **Mã kỹ thuật (Script key)**: `jingxin_jue`
- **Skill ID**: `33` | **Nhánh**: `Bổ Trợ & Phòng Thủ (Support & Defense)` | **Loại**: `Bị động (Passive)`
- **Cấp độ yêu cầu**: Level `20` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tâm cảnh tĩnh lặng như nước. Tăng độ chính xác cực cao (+900%) và gia tăng thời gian thọ thương (co giật) của kẻ địch khi trúng đòn.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,95},{20,900}},{{1,18*120},{20,18*180}}}` |
| `do_hurt_p` | do_hurt_p | `{{{1,1},{2,2},{20,20},{30,30},{40,35},{41,35}},{{1,18},{2,18}}}` |
| `attackratingenhance_v` | attackratingenhance_v | `{{{1,100},{30,5000}},{{1,-1},{2,-1}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,5},{20,20}}}` |

### 3.21 [40] Đoạn Hồn Thích (断魂刺)
- **Mã kỹ thuật (Script key)**: `duanhun_ci`
- **Skill ID**: `40` | **Nhánh**: `Kỹ Năng Cưỡi Ngựa Khống Chế (Charge & Stun)` | **Loại**: `Chủ động trên ngựa (Active Horse Skill)`
- **Cấp độ yêu cầu**: Level `40` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng trứ danh số 1 của Thiên Vương. Lao vút áp sát đối phương với vận tốc ánh sáng, tỉ lệ chí mạng lên tới 80% và gây choáng (Stun) 40% - 60% lập tức.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsenhance_p` | physicsenhance_p | `{{{1,25},{20,215}}}` |
| `seriesdamage_p` | seriesdamage_p | `{{{1,1},{20,50}}}` |
| `stun_p` | stun_p | `{{{1,16},{20,40},{30,60}},{{1,7},{20,27},{25,42},{26,43}}}` |
| `skill_param1_v` | skill_param1_v | `{{{1,4},{5,12},{20,24},{28,31},{31,31}}}` |
| `skill_param2_v` | skill_param2_v | `{{{1,18},{20,1},{21,1}}}` |
| `deadlystrike_p` | deadlystrike_p | `{{{1,4},{20,80}}}` |
| `missle_speed_v` | missle_speed_v | `{{{1,22},{20,30},{21,32},{22,32}}}` |
| `skill_attackradius` | skill_attackradius | `{{{1,22*16},{20,60*16},{21,60*16}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{20,20}}}` |

### 3.22 [42] Kim Chung Trạo (金钟罩)
- **Mã kỹ thuật (Script key)**: `jinzhong_zhao`
- **Skill ID**: `42` | **Nhánh**: `Bổ Trợ & Phòng Thủ (Support & Defense)` | **Loại**: `Chủ động buff hộ thể (Active Buff)`
- **Cấp độ yêu cầu**: Level `50` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Khí công kim cương bất hoại. Tăng 50% Kháng Vật Lý, 49% Kháng Độc, 45% Kháng Băng, nhưng giảm 15% Kháng Hỏa trong thời gian duy trì.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsres_p` | physicsres_p | `{{{1,12},{20,50}},{{1,18*120},{20,18*180}}}` |
| `poisonres_p` | poisonres_p | `{{{1,12},{20,49}},{{1,18*120},{20,18*180}}}` |
| `coldres_p` | coldres_p | `{{{1,7},{20,45}},{{1,18*120},{20,18*180}}}` |
| `fireres_p` | fireres_p | `{{{1,-5},{20,-15},{21,-15}},{{1,18*120},{20,18*180}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,12},{20,40}}}` |

### 3.23 [36] Thiên Vương Chiến Ý (天王战意)
- **Mã kỹ thuật (Script key)**: `tianwang_zhanyi`
- **Skill ID**: `36` | **Nhánh**: `Kỹ Năng Trấn Phái (Ultimate Passive)` | **Loại**: `Bị động Trấn Phái Cấp 60 (Zhenpai Passive)`
- **Cấp độ yêu cầu**: Level `60` | **Cấp độ tối đa**: Level `30`
- **Mô tả**: Trấn phái đệ nhất võ lâm của Thiên Vương Bang. Tăng vĩnh viễn tới 185% máu tối đa, +60% tỉ lệ chí mạng, +65 tốc độ đánh, tăng 20% sát thương lên hệ Mộc và giảm 20% sát thương nhận từ hệ Mộc.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `lifemax_p` | lifemax_p | `{{{1,21},{30,185}},{{1,-1},{30,-1}}}` |
| `lifemax_yan_p` | lifemax_yan_p | `{{{1,21},{35,160},{36,160}},{{1,-1},{30,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,5},{30,60},{40,78}},{{1,-1},{30,-1}}}` |
| `attackspeed_v` | attackspeed_v | `{{{1,5},{30,65}},{{1,-1},{30,-1}}}` |
| `anti_hitrecover` | anti_hitrecover | `{{{1,1},{50,50},{51,50}},{{1,-1},{2,-1}}}` |
| `me2wooddamage_p` | me2wooddamage_p | `{{{1,1},{30,20},{31,20}},{{1,-1},{2,-1}}}` |
| `wood2medamage_p` | wood2medamage_p | `{{{1,1},{30,20},{31,20}},{{1,-1},{2,-1}}}` |
| `returnres_p` | returnres_p | `{{{1,1},{20,20},{30,30},{31,30}},{{1,-1},{20,-1}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,10},{30,50}}}` |
| `anti_block_rate` | anti_block_rate | `{{{1,1},{20,20},{30,30},{31,30}},{{1,-1},{20,-1}}}` |
| `do_hurt_p` | do_hurt_p | `{{{1,0},{39,0},{40,20},{41,20}},{{1,-1},{20,-1}}}` |

---

## 4. Ma Trận Hỗ Trợ Tương Hỗ Đa Tầng (Skill Synergy Matrix)

Điểm cốt lõi tạo nên sức mạnh của Thiên Vương Bang là **hệ thống kỹ năng cấp thấp hỗ trợ tăng phần trăm sát thương cho kỹ năng cấp cao (Cấp 90 và Cấp 150)**:

### 4.1 Bảng Tương Hỗ Cho Nhánh ĐAO (Blade)
| Chiêu Xuất Trận | Chiêu Hỗ Trợ Cấp Thấp | Cấp Skill Hỗ Trợ | % Sát Thương Cộng Hưởng (`addskilldamage`) |
| :--- | :--- | :---: | :---: |
| **Phá Thiên Trảm (Cấp 90)** | **Vô Tâm Trảm** (`wuxin_zhan`) | 20 | **+80%** |
|  | **Kinh Lôi Trảm** (`jinglei_zhan`) | 20 | **+60%** |
|  | **Phách Phong Trảm** (`pofeng_zhan`) | 20 | **+70%** |
|  | **TỔNG HỖ TRỢ CHIÊU 90** | — | **+210%** |
| **Hào Hùng Trảm (Cấp 150)** | **Vô Tâm Trảm** (`wuxin_zhan`) | 20 | **+67%** |
|  | **Kinh Lôi Trảm** (`jinglei_zhan`) | 20 | **+50%** |
|  | **Phách Phong Trảm** (`pofeng_zhan`) | 20 | **+58%** *(Cấp 27 là +98%)* |
|  | **Phá Thiên Trảm** (`potian_zhan`) | 20 | **+35%** |
|  | **TỔNG HỖ TRỢ CHIÊU 150** | — | **+210%** *(Lên tới +250% nếu có đồ +skill)* |

### 4.2 Bảng Tương Hỗ Cho Nhánh CHÙY (Hammer)
| Chiêu Xuất Trận | Chiêu Hỗ Trợ Cấp Thấp | Cấp Skill Hỗ Trợ | % Sát Thương Cộng Hưởng (`addskilldamage`) |
| :--- | :--- | :---: | :---: |
| **Truy Tinh Trục Nguyệt (Cấp 90)** | **Dương Quan Tam Điệp** (`yangguan_sandie`) | 20 | **+65%** |
|  | **Hồi Phong Lạc Nhạn** (`huifeng_luoyan`) | 20 | **+60%** |
|  | **TỔNG HỖ TRỢ CHIÊU 90** | — | **+125%** |
| **Tung Hoành Bát Hoang (Cấp 150)** | **Dương Quan Tam Điệp** (`yangguan_sandie`) | 20 | **+54%** |
|  | **Hồi Phong Lạc Nhạn** (`huifeng_luoyan`) | 20 | **+50%** |
|  | **TỔNG HỖ TRỢ CHIÊU 150** | — | **+104%** |

---

## 5. Công Thức Sát Thương Ngoại Công & Cơ Chế Sát Thương Chí Mạng

### 5.1 Bốn Tầng Cộng Dồn Tỉ Lệ Chí Mạng (%)
$$\text{Tổng Tỉ Lệ Chí Mạng} = \text{Skill Cấp 10 (15\%)} + \text{Trấn Phái 60 (60\%)} + \text{Skill Xuất Chiêu (25\% - 80\%)} + \text{Trang Bị (10\% - 20\%)}$$

- **Huyết Chiến Bát Phương / Phá Thiên Trảm / Truy Tinh Trục Nguyệt (Chiêu 90)**: Đạt **90% - 100%** tỉ lệ chí mạng.
- **Đoạn Hồn Thích (Cấp 40)**: Tỉ lệ đạt **136% -> 100% chắc chắn nổ chí mạng** kèm choáng.
- **Hệ số sát thương khi Chí Mạng**: **Nhân đôi toàn bộ ($D_{\text{crit}} = D_{\text{base}} \times 2$)**.

### 5.2 Hai Mô Hình Tính Sát Thương Lực Tay (Damage Formulas)

#### Mô hình A: Công Thức Cộng Gộp Tuyến Tính (Additive Model)
$$\text{Damage} = (W + B) \times \left(1 + \frac{\text{SM}}{100}\right) \times \left(1 + \frac{S_{\text{passive}} + S_{\text{active}} + S_{\text{synergy}} + S_{\text{gear}}}{100}\right) + E_{\text{element}}$$

#### Mô hình B: Cơ Chế Engine C++ Kingsoft (Multiplicative Layer Model)
$$\text{Damage} = \left[W \times \left(1 + \frac{S_{\text{passive}} + S_{\text{gear\_pct}}}{100}\right) + B\right] \times \left(1 + \frac{\text{SM}}{100}\right) \times \left(1 + \frac{S_{\text{active}} + S_{\text{synergy}}}{100}\right) + E_{\text{element}}$$

> [!TIP]
> Khi so sánh với codebase server khác (như JX Linux, JX Win32, JX2), cần kiểm tra xem hàm `KPlayer::GetDamage()` hay `KSkill::GetDamage()` áp dụng phép nhân theo **Mô hình A (Cộng gộp)** hay **Mô hình B (Nhân tầng)**, vì Mô hình B sẽ cho ra lực tay hiển thị gấp khoảng 1.8 - 2.5 lần so với Mô hình A.