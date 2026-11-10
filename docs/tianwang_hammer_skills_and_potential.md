# Báo Cáo Kỹ Thuật: THIÊN VƯƠNG CHÙY PHÁP (Level 10 - 150) & Công Thức Điểm Tiềm Năng

> **Mục đích tài liệu**: Chuẩn tham chiếu (Ground Truth Reference) cho nhánh **Thiên Vương Chùy (Hammer)**, dùng đối chiếu độc lập với các codebase Võ Lâm Truyền Kỳ khác.

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

## 2. Bảng Tra Cứu Kỹ Năng Nhánh Chùy (Level 10 - 150) & Kỹ Năng Hỗ Trợ

| STT | Kỹ Năng | Tên Hán Tự | Mã Script | Skill ID | Cấp Y/C | Dạng Kỹ Năng |
| :-: | :--- | :--- | :--- | :-: | :-: | :--- |
| 1 | **Thiên Vương Chùy Pháp** | 天王锤法 | `tianwang_chuifa` | 26 | Cấp 10 | Bị động cơ bản (Passive) |
| 2 | **Trảm Long Quyết** | 斩龙诀 | `zhanlong_jue` | 29 | Cấp 30 | Chủ động tấn công (Active) |
| 3 | **Hồi Phong Lạc Nhạn** | 回风落雁 | `huifeng_luoyan` | 30 | Cấp 30 | Chủ động tấn công (Active) |
| 4 | **Dương Quan Tam Điệp** | 阳关三叠 | `yangguan_sandie` | 35 | Cấp 60 | Chủ động tấn công (Active) |
| 5 | **Truy Tinh Trục Nguyệt** | 追星逐月 | `zhuixing_zhuyue` | 323 | Cấp 90 | Chủ động tấn công (Active - Cấp 90) |
| 6 | **Truy Phong Quyết** | 追风诀 | `zhuifeng_jue` | 325 | Cấp 120 | Chủ động tấn công (Active - Cấp 120) |
| 7 | **Tung Hoành Bát Hoang** | 锤天王150 / 纵横八荒 | `chuitianwang150` | 1059 | Cấp 150 | Chủ động tấn công (Active - Cấp 150) |
| 8 | **Tĩnh Tâm Quyết** | 静心诀 | `jingxin_jue` | 33 | Cấp 20 | Bị động (Passive) |
| 9 | **Đoạn Hồn Thích** | 断魂刺 | `duanhun_ci` | 40 | Cấp 40 | Chủ động cưỡi ngựa (Active Horse Skill) |
| 10 | **Kim Chung Trạo** | 金钟罩 | `jinzhong_zhao` | 42 | Cấp 50 | Chủ động buff hộ thể (Active Buff) |
| 11 | **Thiên Vương Chiến Ý** | 天王战意 | `tianwang_zhanyi` | 36 | Cấp 60 | Bị động Trấn Phái Cấp 60 (Zhenpai Passive) |

---

## 3. Đặc Tả Thuộc Tính Ma Pháp Chi Tiết Nhánh Chùy (Hammer Skills Specification)

### 3.1 [26] Thiên Vương Chùy Pháp (天王锤法)
- **Mã kỹ thuật (Script key)**: `tianwang_chuifa`
- **Skill ID**: `26` | **Dạng**: `Bị động cơ bản (Passive)`
- **Cấp độ yêu cầu**: Level `10` | **Cấp độ tối đa**: Level `20`
- **Mô tả**: Kỹ năng chùy pháp cơ bản môn phái. Tăng vĩnh viễn sát thương vật lý vũ khí (+275%), độ chính xác và xác suất đòn chí mạng (+15%) khi cầm Chùy.

| Thuộc Tính Engine | Mã Lệnh Game | Cấu Hình Nội Suy Chi Tiết (Raw Script Data) |
| :--- | :--- | :--- |
| `addphysicsdamage_p` | addphysicsdamage_p | `{{{1,25},{20,275}},{{1,-1},{2,-1}},{{1,4},{2,4}}}` |
| `attackratingenhance_p` | attackratingenhance_p | `{{{1,15},{20,72}},{{1,-1},{2,-1}}}` |
| `deadlystrikeenhance_p` | deadlystrikeenhance_p | `{{{1,2},{20,15}},{{1,-1},{2,-1}}}` |

### 3.2 [29] Trảm Long Quyết (斩龙诀)
- **Mã kỹ thuật (Script key)**: `zhanlong_jue`
- **Skill ID**: `29` | **Dạng**: `Chủ động tấn công (Active)`
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

### 3.3 [30] Hồi Phong Lạc Nhạn (回风落雁)
- **Mã kỹ thuật (Script key)**: `huifeng_luoyan`
- **Skill ID**: `30` | **Dạng**: `Chủ động tấn công (Active)`
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

### 3.4 [35] Dương Quan Tam Điệp (阳关三叠)
- **Mã kỹ thuật (Script key)**: `yangguan_sandie`
- **Skill ID**: `35` | **Dạng**: `Chủ động tấn công (Active)`
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

### 3.5 [323] Truy Tinh Trục Nguyệt (追星逐月)
- **Mã kỹ thuật (Script key)**: `zhuixing_zhuyue`
- **Skill ID**: `323` | **Dạng**: `Chủ động tấn công (Active - Cấp 90)`
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

### 3.6 [325] Truy Phong Quyết (追风诀)
- **Mã kỹ thuật (Script key)**: `zhuifeng_jue`
- **Skill ID**: `325` | **Dạng**: `Chủ động tấn công (Active - Cấp 120)`
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

### 3.7 [1059] Tung Hoành Bát Hoang (锤天王150 / 纵横八荒)
- **Mã kỹ thuật (Script key)**: `chuitianwang150`
- **Skill ID**: `1059` | **Dạng**: `Chủ động tấn công (Active - Cấp 150)`
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

## 5. Ma Trận Hỗ Trợ Tương Hỗ Nhánh Chùy

| Chiêu Xuất Trận | Chiêu Hỗ Trợ Cấp Thấp | Cấp Hỗ Trợ | % Sát Thương Tương Hỗ (`addskilldamage`) | Hiệu Ứng Đi Kèm |
| :--- | :--- | :---: | :---: | :--- |
| **Truy Tinh Trục Nguyệt (Cấp 90)** | Dương Quan Tam Điệp (`yangguan_sandie`) | 20 | **+65%** | Tỉ lệ choáng cực cao |
|  | Hồi Phong Lạc Nhạn (`huifeng_luoyan`) | 20 | **+60%** | Cú bổ nện uy lực sốc bạo kích |
|  | **TỔNG HỖ TRỢ TRUY TINH TRỤC NGUYỆT** | — | **+125%** | — |
| **Tung Hoành Bát Hoang (Cấp 150)** | Dương Quan Tam Điệp (`yangguan_sandie`) | 20 | **+54%** | Đập nổ xung chấn diện rộng |
|  | Hồi Phong Lạc Nhạn (`huifeng_luoyan`) | 20 | **+50%** | Tỉ lệ chí mạng tự thân lên tới 50% - 71% |
|  | **TỔNG HỖ TRỢ TUNG HOÀNH BÁT HOANG** | — | **+104%** | — |

---

## 6. Công Thức Tính Sát Thương Lực Tay & Chí Mạng Nhánh Chùy

### 6.1 Bốn Tầng Chí Mạng Nhánh Chùy
- Chùy Pháp Cấp 10: **+15%**
- Thiên Vương Chiến Ý Cấp 60: **+60%**
- Truy Tinh Trục Nguyệt (90): **+25%** | Tung Hoành Bát Hoang (150): **+50% - 71%**
- Trang bị (Hám Thiên Thần Chùy HKMP / Dây chuyền): **+10% - 15%**

$$\Rightarrow \text{Tổng Tỉ Lệ Chí Mạng Nhánh Chùy} = 15\% + 60\% + 50\% + 10\% = \mathbf{135\%} \implies \mathbf{100\%} \text{ Chí Mạng Mọi Cú Bổ Chùy!}$$

### 6.2 Hai Mô Hình Tính Sát Thương
- **Mô hình A (Cộng gộp)**: $\text{Damage} = (W + B) \times (1 + \frac{\text{SM}}{100}) \times (1 + \frac{S_{\text{passive}} + S_{\text{active}} + S_{\text{synergy}} + S_{\text{gear}}}{100}) + E$
- **Mô hình B (Nhân tầng Engine C++)**: $\text{Damage} = [W \times (1 + \frac{S_{\text{passive}} + S_{\text{gear\_pct}}}{100}) + B] \times (1 + \frac{\text{SM}}{100}) \times (1 + \frac{S_{\text{active}} + S_{\text{synergy}}}{100}) + E$