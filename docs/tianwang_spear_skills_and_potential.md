# Báo Cáo Kỹ Thuật: THIÊN VƯƠNG THƯƠNG PHÁP (Level 10 - 150) & Công Thức Điểm Tiềm Năng

> **Mục đích tài liệu**: Chuẩn tham chiếu (Ground Truth Reference) cho nhánh **Thiên Vương Thương (Spear)**, dùng đối chiếu độc lập với các codebase Võ Lâm Truyền Kỳ khác.

---

## 1. Công Thức & Cơ Chế Điểm Tiềm Năng Hệ KIM

Thiên Vương Bang thuộc **Hệ KIM**, sở hữu hệ số sinh khí và lượng máu tự nhiên cao nhất toàn cõi võ lâm.

### 1.1 Bảng Hệ Số Tăng Trưởng Gốc Hệ KIM (Trích xuất từ `Client_VLTK_SHXT/settings/npc/player/level_add.txt`)

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

### 1.2 Kháng Tính Tự Nhiên Ban Đầu & Khung Hình (`basevalue.ini`)
- **Kháng Độc (`poisonres`)**: **+25%** *(Kim khắc Mộc - Thiên Vương bẩm sinh kháng độc tự nhiên)*.
- **Kháng Hỏa (`fireres`)**: **-25%** *(Hỏa khắc Kim - Thiên Vương bẩm sinh sợ hỏa công của Cái Bang/Thiên Nhẫn)*.
- **Kháng Băng, Lôi, Vật Lý**: **0%**.
- **Thời gian thọ thương co giật khi trúng đòn**: `HurtFrame = 12 frames` (khoảng 0.67 giây).
- **Tốc độ chạy cơ bản**: `RunSpeed = 10` | **Tốc độ xuất chiêu / tấn công chuẩn**: `AttackFrame = 18`, `CastFrame = 18`.

### 1.3 Công Thức Toán Học Tính Máu Thực Tế
$$\text{Máu Cơ Bản} = (\text{Level} \times 4) + (\text{Điểm Sinh Khí} \times 8) + \text{Máu Từ Trang Bị}$$
$$\text{Máu Thực Tế Khi Bật Chiến Ý} = \text{Máu Cơ Bản} \times \left(1 + \frac{\text{% Máu Từ Thiên Vương Chiến Ý}}{100}\right)$$
*(Ở Cấp 30 Chiến Ý, lượng máu được nhân thêm tới +185%, tức gấp gần 3 lần lượng máu cơ bản!)*

---

## 2. Bảng Tra Cứu Kỹ Năng Nhánh Thương (Level 10 - 150) & Kỹ Năng Hỗ Trợ

| STT | Kỹ Năng | Tên Hán Tự | Mã Script | Skill ID | Cấp Y/C | Dạng Kỹ Năng |
| :-: | :--- | :--- | :--- | :-: | :-: | :--- |
| 1 | **Thiên Vương Thương Pháp** | 天王枪法 | `tianwang_qiangfa` | 23 | Cấp 10 | Bị động cơ bản (Passive) |
| 2 | **Dương Gia Thương Pháp / Hành Vân Quyết** | 行云诀 | `xingyun_jue` | 31 | Cấp 30 | Chủ động tấn công (Active) |
| 3 | **Vô Tâm Trảm** | 无心斩 | `wuxin_zhan` | 32 | Cấp 60 | Chủ động tấn công (Active) |
| 4 | **Huyết Chiến Bát Phương** | 血战八方 | `xuezhan_bafang` | 41 | Cấp 90 | Chủ động tấn công (Active - Cấp 90) |
| 5 | **Thừa Long Quyết** | 乘龙诀 | `chenglong_jue` | 324 | Cấp 120 | Chủ động tấn công (Active - Cấp 120) |
| 6 | **Bá Vương Tán Kim** | 枪天150 / 霸王錾金 | `qiangtianwang150` | 1060 | Cấp 150 | Chủ động tấn công (Active - Cấp 150) |
| 7 | **Tĩnh Tâm Quyết** | 静心诀 | `jingxin_jue` | 33 | Cấp 20 | Bị động (Passive) |
| 8 | **Đoạn Hồn Thích** | 断魂刺 | `duanhun_ci` | 40 | Cấp 40 | Chủ động cưỡi ngựa (Active Horse Skill) |
| 9 | **Kim Chung Trạo** | 金钟罩 | `jinzhong_zhao` | 42 | Cấp 50 | Chủ động buff hộ thể (Active Buff) |
| 10 | **Thiên Vương Chiến Ý** | 天王战意 | `tianwang_zhanyi` | 36 | Cấp 60 | Bị động Trấn Phái Cấp 60 (Zhenpai Passive) |

---

## 3. Đặc Tả Thuộc Tính Ma Pháp Chi Tiết Nhánh Thương (Spear Skills Specification)

### 3.1 [23] Thiên Vương Thương Pháp (天王枪法)
- **Mã kỹ thuật (Script key)**: `tianwang_qiangfa`
- **Skill ID**: `23` | **Dạng**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng thương pháp cơ bản môn phái. Tăng vĩnh viễn sát thương vật lý vũ khí (+315%), độ chính xác (+270%) và xác suất ra đòn chí mạng (+15%) khi dùng Thương.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,25},{20,315}},{{1,-1},{2,-1}},{{1,3},{2,3}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,75},{20,270}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.2 [31] Dương Gia Thương Pháp / Hành Vân Quyết (行云诀)
- **Mã kỹ thuật (Script key)**: `xingyun_jue`
- **Skill ID**: `31` | **Dạng**: `Chủ động tấn công (Active)`
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
- **Skill ID**: `32` | **Dạng**: `Chủ động tấn công (Active)`
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
- **Skill ID**: `41` | **Dạng**: `Chủ động tấn công (Active - Cấp 90)`
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
- **Skill ID**: `324` | **Dạng**: `Chủ động tấn công (Active - Cấp 120)`
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
- **Skill ID**: `1060` | **Dạng**: `Chủ động tấn công (Active - Cấp 150)`
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


## 4. Đặc Tả Thuộc Tính Ma Pháp Kỹ Năng Dùng Chung & Trấn Phái

### 4.1 [33] Tĩnh Tâm Quyết (静心诀)
- **Mã kỹ thuật (Script key)**: `jingxin_jue`
- **Skill ID**: `33` | **Dạng**: `Bị động (Passive)`
- **Cấp độ yêu cầu**: Level `20` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tâm cảnh tĩnh lặng như nước. Tăng độ chính xác cực cao (+900%) và gia tăng thời gian thọ thương (co giật) của kẻ địch khi trúng đòn.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,95},{20,900}},{{1,18*120},{20,18*180}}}` |
| `do_hurt_p` | do_hurt_p | `{{{1,1},{2,2},{20,20},{30,30},{40,35},{41,35}},{{1,18},{2,18}}}` |
| `attackratingenhance_v` | attackratingenhance_v | `{{{1,100},{30,5000}},{{1,-1},{2,-1}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,5},{20,20}}}` |

### 4.2 [40] Đoạn Hồn Thích (断魂刺)
- **Mã kỹ thuật (Script key)**: `duanhun_ci`
- **Skill ID**: `40` | **Dạng**: `Chủ động cưỡi ngựa (Active Horse Skill)`
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

### 4.3 [42] Kim Chung Trạo (金钟罩)
- **Mã kỹ thuật (Script key)**: `jinzhong_zhao`
- **Skill ID**: `42` | **Dạng**: `Chủ động buff hộ thể (Active Buff)`
- **Cấp độ yêu cầu**: Level `50` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Khí công kim cương bất hoại. Tăng 50% Kháng Vật Lý, 49% Kháng Độc, 45% Kháng Băng, nhưng giảm 15% Kháng Hỏa trong thời gian duy trì.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `physicsres_p` | physicsres_p | `{{{1,12},{20,50}},{{1,18*120},{20,18*180}}}` |
| `poisonres_p` | poisonres_p | `{{{1,12},{20,49}},{{1,18*120},{20,18*180}}}` |
| `coldres_p` | coldres_p | `{{{1,7},{20,45}},{{1,18*120},{20,18*180}}}` |
| `fireres_p` | fireres_p | `{{{1,-5},{20,-15},{21,-15}},{{1,18*120},{20,18*180}}}` |
| `skill_cost_v` | skill_cost_v | `{{{1,12},{20,40}}}` |

### 4.4 [36] Thiên Vương Chiến Ý (天王战意)
- **Mã kỹ thuật (Script key)**: `tianwang_zhanyi`
- **Skill ID**: `36` | **Dạng**: `Bị động Trấn Phái Cấp 60 (Zhenpai Passive)`
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

## 5. Ma Trận Hỗ Trợ Tương Hỗ Nhánh Thương & Đoạn Hồn Thích

| Kỹ Năng Xuất Chiêu | Kỹ Năng Hỗ Trợ | Cấp Hỗ Trợ | % Sát Thương Tương Hỗ | Hiệu Ứng Đi Kèm |
| :--- | :--- | :---: | :---: | :--- |
| **Huyết Chiến Bát Phương (Cấp 90)** | Hồi Phong Lạc Nhạn (`huifeng_luoyan`) | 20 | **+15%** | Đâm liên hoàn 5 đòn chớp nhoáng |
| **Đoạn Hồn Thích (Cấp 40)** | Tự thân + Thương pháp | 20 | **+80% Chí Mạng** | Tỉ lệ gây choáng (Stun) 40% - 60% |
| **Bá Vương Tán Kim (Cấp 150)** | Cấp 20 / 26 | 20 | Tăng 40% - 54% Chí Mạng | Đâm xuyên thấu 3 tia diện rộng |

---

## 6. Công Thức Tính Sát Thương Lực Tay & Chí Mạng Nhánh Thương

### 6.1 Bốn Tầng Chí Mạng Nhánh Thương
- Thương Pháp Cấp 10: **+15%**
- Thiên Vương Chiến Ý Cấp 60 (30 điểm): **+60%**
- Huyết Chiến Bát Phương Cấp 90: **+25%**
- Trang bị (Vũ khí / Dây chuyền): **+10% - 15%**

$$\Rightarrow \text{Tổng Tỉ Lệ Chí Mạng Huyết Chiến Bát Phương} = 15\% + 60\% + 25\% + 10\% = \mathbf{110\%} \implies \mathbf{100\%} \text{ Đòn Đâm Ra Đều Chí Mạng!}$$

### 6.2 Hai Mô Hình Tính Sát Thương
- **Mô hình A (Cộng gộp)**: $\text{Damage} = (W + B) \times (1 + \frac{\text{SM}}{100}) \times (1 + \frac{S_{\text{passive}} + S_{\text{active}} + S_{\text{gear}}}{100}) + E$
- **Mô hình B (Nhân tầng Engine C++)**: $\text{Damage} = [W \times (1 + \frac{S_{\text{passive}} + S_{\text{gear\_pct}}}{100}) + B] \times (1 + \frac{\text{SM}}{100}) \times (1 + \frac{S_{\text{active}}}{100}) + E$