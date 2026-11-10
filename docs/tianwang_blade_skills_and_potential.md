# Báo Cáo Kỹ Thuật: THIÊN VƯƠNG ĐAO PHÁP (Level 10 - 150) & Công Thức Điểm Tiềm Năng

> **Mục đích tài liệu**: Chuẩn tham chiếu (Ground Truth Reference) cho nhánh **Thiên Vương Đao (Blade)**, dùng đối chiếu độc lập với các codebase Võ Lâm Truyền Kỳ khác.

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

## 2. Bảng Tra Cứu Kỹ Năng Nhánh Đao (Level 10 - 150) & Kỹ Năng Hỗ Trợ

| STT | Kỹ Năng | Tên Hán Tự | Mã Script | Skill ID | Cấp Y/C | Dạng Kỹ Năng |
| :-: | :--- | :--- | :--- | :-: | :-: | :--- |
| 1 | **Thiên Vương Đao Pháp** | 天王刀法 | `tianwang_daofa` | 24 | Cấp 10 | Bị động cơ bản (Passive) |
| 2 | **Kinh Lôi Trảm** | 惊雷斩 | `jinglei_zhan` | 34 | Cấp 30 | Chủ động tấn công (Active) |
| 3 | **Phách Phong Trảm** | 泼风斩 | `pofeng_zhan` | 37 | Cấp 60 | Chủ động tấn công (Active) |
| 4 | **Vô Tâm Trảm (Kỹ Năng Tương Hỗ Đao)** | 无心斩 | `wuxin_zhan` | 32 | Cấp 60 | Hỗ trợ tương hỗ Đao Pháp (Synergy) |
| 5 | **Phá Thiên Trảm** | 破天斩 | `potian_zhan` | 322 | Cấp 90 | Chủ động tấn công (Active - Cấp 90) |
| 6 | **Đảo Hư Thiên** | 倒虚天 | `daoxutian` | 708 | Cấp 120 | Chủ động Hộ Thân (Buff - Cấp 120) |
| 7 | **Hào Hùng Trảm** | 刀天150 / 豪雄斩 | `daotianwang150` | 1058 | Cấp 150 | Chủ động tấn công (Active - Cấp 150) |
| 8 | **Tĩnh Tâm Quyết** | 静心诀 | `jingxin_jue` | 33 | Cấp 20 | Bị động (Passive) |
| 9 | **Đoạn Hồn Thích** | 断魂刺 | `duanhun_ci` | 40 | Cấp 40 | Chủ động cưỡi ngựa (Active Horse Skill) |
| 10 | **Kim Chung Trạo** | 金钟罩 | `jinzhong_zhao` | 42 | Cấp 50 | Chủ động buff hộ thể (Active Buff) |
| 11 | **Thiên Vương Chiến Ý** | 天王战意 | `tianwang_zhanyi` | 36 | Cấp 60 | Bị động Trấn Phái Cấp 60 (Zhenpai Passive) |

---

## 3. Đặc Tả Thuộc Tính Ma Pháp Chi Tiết Nhánh Đao (Blade Skills Specification)

### 3.1 [24] Thiên Vương Đao Pháp (天王刀法)
- **Mã kỹ thuật (Script key)**: `tianwang_daofa`
- **Skill ID**: `24` | **Dạng**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng đao pháp cơ bản môn phái. Tăng vĩnh viễn 300% sát thương vật lý vũ khí, độ chính xác và 15% chí mạng khi dùng Đao.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,50},{20,300}},{{1,-1},{2,-1}},{{1,1},{2,1}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,15},{20,72}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.2 [34] Kinh Lôi Trảm (惊雷斩)
- **Mã kỹ thuật (Script key)**: `jinglei_zhan`
- **Skill ID**: `34` | **Dạng**: `Chủ động tấn công (Active)`
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

### 3.3 [37] Phách Phong Trảm (泼风斩)
- **Mã kỹ thuật (Script key)**: `pofeng_zhan`
- **Skill ID**: `37` | **Dạng**: `Chủ động tấn công (Active)`
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

### 3.4 [32] Vô Tâm Trảm (Kỹ Năng Tương Hỗ Đao) (无心斩)
- **Mã kỹ thuật (Script key)**: `wuxin_zhan`
- **Skill ID**: `32` | **Dạng**: `Hỗ trợ tương hỗ Đao Pháp (Synergy)`
- **Cấp độ yêu cầu**: Level `60` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Chiêu thức đâm hỗ trợ quan trọng, tăng thêm +80% sát thương cho Phá Thiên Trảm 90 và +67% cho Hào Hùng Trảm 150.

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

### 3.5 [322] Phá Thiên Trảm (破天斩)
- **Mã kỹ thuật (Script key)**: `potian_zhan`
- **Skill ID**: `322` | **Dạng**: `Chủ động tấn công (Active - Cấp 90)`
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

### 3.6 [708] Đảo Hư Thiên (倒虚天)
- **Mã kỹ thuật (Script key)**: `daoxutian`
- **Skill ID**: `708` | **Dạng**: `Chủ động Hộ Thân (Buff - Cấp 120)`
- **Cấp độ yêu cầu**: Level `120` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Tuyệt kỹ hộ thân tối thượng của Thiên Vương Đao. Tăng 10% tất cả kháng tính, tăng trần kháng tối đa +5%, tăng tốc độ hồi phục sinh lực +35% và bỏ qua hiệu ứng khống chế của đối thủ.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `allres_p` | allres_p | `{{{1,1},{20,10},{21,10}},{{1,-1},{2,-1}}}` |
| `allresmax_p` | allresmax_p | `{{{1,1},{20,5},{21,5}},{{1,-1},{2,-1}}}` |
| `lifereplenish_p` | lifereplenish_p | `{{{1,1},{20,35},{28,50},{29,50}},{{1,-1},{2,-1}}}` |
| `ignoreskill_p` | ignoreskill_p | `{{{1,1},{28,100},{29,100}},{{1,-1},{2,-1}}}` |
| `skill_skillexp_v` | skill_skillexp_v | `{{	{1,17851239}` |

### 3.7 [1058] Hào Hùng Trảm (刀天150 / 豪雄斩)
- **Mã kỹ thuật (Script key)**: `daotianwang150`
- **Skill ID**: `1058` | **Dạng**: `Chủ động tấn công (Active - Cấp 150)`
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

## 5. Ma Trận Hỗ Trợ Tương Hỗ Đa Tầng Nhánh Đao (Full Blade Synergy Matrix)

Nhánh Đao là nhánh sở hữu hệ thống hỗ trợ tương hỗ mạnh mẽ nhất với **4 kỹ năng cùng lúc buff sát thương cho Hào Hùng Trảm 150**:

| Chiêu Xuất Trận | Chiêu Hỗ Trợ Cấp Thấp | Cấp Hỗ Trợ | % Sát Thương Tương Hỗ (`addskilldamage`) |
| :--- | :--- | :---: | :---: |
| **Phá Thiên Trảm (Cấp 90)** | Vô Tâm Trảm (`wuxin_zhan`) | 20 | **+80%** |
|  | Kinh Lôi Trảm (`jinglei_zhan`) | 20 | **+60%** |
|  | Phách Phong Trảm (`pofeng_zhan`) | 20 | **+70%** |
|  | **TỔNG HỖ TRỢ PHÁ THIÊN TRẢM** | — | **+210%** |
| **Hào Hùng Trảm (Cấp 150)** | Vô Tâm Trảm (`wuxin_zhan`) | 20 | **+67%** |
|  | Kinh Lôi Trảm (`jinglei_zhan`) | 20 | **+50%** |
|  | Phách Phong Trảm (`pofeng_zhan`) | 20 | **+58%** *(Cấp 27 là +98%)* |
|  | Phá Thiên Trảm (`potian_zhan`) | 20 | **+35%** |
|  | **TỔNG HỖ TRỢ HÀO HÙNG TRẢM** | — | **+210%** *(Lên tới +250% nếu có đồ +skill)* |

---

## 6. Công Thức Tính Sát Thương Lực Tay & Chí Mạng Nhánh Đao

### 6.1 Cơ Chế Chí Mạng Nhánh Đao
- Đao Pháp Cấp 10: **+15%** | Trấn Phái Cấp 60: **+60%** | Phá Thiên Trảm: **+25%** / Hào Hùng Trảm: **+30%** | Đồ: **+10%**
$$\Rightarrow \text{Tổng Tỉ Lệ Chí Mạng} = 15\% + 60\% + 25\% + 10\% = \mathbf{110\%} \implies \mathbf{100\%} \text{ Chí Mạng!}$$

### 6.2 So Sánh Lực Tay Cấp 160 Cầm Ngự Long Bảo Đao (Đao Hoàng Kim Môn Phái)
| Lối Tăng Điểm | Mô Hình Tính | Lực Tay F3 Hiển Thị (Min - Max) | Sát Thương Chí Mạng (x2) |
| :--- | :--- | :---: | :---: |
| **Tank Sinh Tồn (SM 320)** | Mô hình A (Cộng gộp) | **$5.850 - 11.000$** | **$11.700 - 22.000$** |
|  | Mô hình B (Engine C++ nhân tầng) | **$10.200 - 25.100$** | **$20.400 - 50.200$** |
| **Thuần Sức Mạnh (SM 600)** | Mô hình A (Cộng gộp) | **$9.700 - 18.300$** | **$19.400 - 36.600$** |
|  | Mô hình B (Engine C++ nhân tầng) | **$16.900 - 41.800$** | **$33.800 - 83.600$** |