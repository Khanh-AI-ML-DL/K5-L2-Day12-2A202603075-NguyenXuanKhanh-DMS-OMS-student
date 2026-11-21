# Danh sách lớp v0 — Nguyễn Xuân Khánh · G08

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**
Các lớp và giá trị dưới đây bám theo Guideline Cabin v1.0 và `labels_cabin_v1.json`.

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face.eye_left, face.eye_right | open / closed / unknown (mỗi mắt riêng) | Phát hiện buồn ngủ (mắt nhắm lâu). `closed` chỉ mô tả khung hình này, không phải kết luận buồn ngủ | Có, trừ khi đốm phản xạ LED hoặc kính che mắt thì ghi `unknown` |
| 2 | face.gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (không nhìn đường quá lâu) và kiểm tra tài xế có quan sát gương | Có, ước lượng từ hướng mắt và đầu. Khi mắt không rõ thì dựa vào đầu hoặc ghi `other` |
| 3 | face.glasses | none / clear / sun / unknown | Chọn cách xử lý mắt (kính phản xạ, kính râm) để giảm cảnh báo sai | Một phần: kính râm có thể trông trong suốt trên NIR nên dễ nhầm với `clear`; không chắc thì `unknown` |
| 4 | face13 (13 điểm mặt, cờ occluded / outside) | tọa độ điểm + cờ che | Ước lượng tư thế đầu và độ mở mắt; cờ cho biết điểm nào model không nên tin | Có trên mặt đủ lớn (từ 60 px). Điểm sau tay, kính hoặc đốm sáng thì đánh cờ, không đặt cho đủ |
| 5 | hand (whose, side, on_wheel) | driver / passenger · left / right · yes / no / unknown | Kiểm tra tay có trên vô lăng không (cảnh báo tiếp quản xe), xem tay đang làm gì | Có, nhìn theo hình dạng. Trên xe tự lái thử nghiệm, `on_wheel = no` là bình thường |
| 6 | phone (state) | held / mounted / lap | Phát hiện dùng điện thoại khi lái | Chỉ khi thấy cạnh, góc hoặc màn hình. Vật tối cầm sát tai mà không thấy hình dạng thì không vẽ |
| 7 | person (driver).seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn, phát hiện đeo sai (dưới nách, sau lưng) | Không chắc: áo tối hoặc bóng tối thì ghi `unknown`, không đoán |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person.seat | driver / front_passenger / rear_left / rear_middle / rear_right (theo xe) | Đếm và xác định vị trí người trên xe; điều khiển túi khí và cảnh báo theo từng ghế | Có (hình dạng). Camera nhìn về sau nên trái ảnh là `rear_right` |
| 2 | person.seatbelt | not_worn / unknown (trên SVIRO) | Nhắc thắt dây an toàn cho từng ghế | Thường không: dây mảnh, tối trên IR; thấy rõ không có dây mới ghi `not_worn`, không thấy thì `unknown` |
| 3 | child_seat | có / không theo ghế; occupied: no / unknown | Nhận biết ghế trẻ em đang lắp, nhắc kiểm tra trẻ có trong ghế; tắt túi khí ghế trước nếu ghế trẻ em ở đó | Có  |
| 4 | infant_seat | có / không theo ghế; facing: rear / front | Nhắc quên trẻ trong xe; tắt túi khí ghế trước khi có ghế em bé quay ngược | Có  |
| 5 | object | type: bag / box / cup / other, theo ghế | Nhắc quên đồ vật; phân biệt đồ vật với người trên ghế để tránh đếm sai | Có theo hình dạng, không dùng màu. Vật nằm trong ghế trẻ em cần box riêng |
| 6 | face (trên ảnh OMS) | chỉ box | Đếm người, hỗ trợ xác nhận người ngồi ghế nào (OMS chỉ cần box) | Có nếu mặt đủ lớn và không bị che |
| 7 | frame_meta (modality, light, camera_blocked) | rgb / ir · day / night / unknown · yes / no | Biết ảnh là loại nào để xử lý đúng; phát hiện camera bị che | Có. `light = unknown` với ảnh dựng |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Khi trong ghế trẻ em hoặc ghế em bé có một hình người (hoặc giống người), thì vẽ thế nào? `child_seat.occupied` chỉ có `no` và `unknown` (4.8, không dùng `yes`), nhưng không có giá trị nào cho ca ghế có người ngồi. Có vẽ thêm `person` bên trong không? GUIDE §3 nói bộ ảnh không có trẻ em ngồi và hình giống trẻ em thì báo coach, không gán.
   Khung ví dụ: `S02_rgb` (mình: `child_seat occupied = no`, kèm `person` và `face` trong cùng ghế; bạn: `occupied = yes`, trái 4.8). `S04_rgb` và `S08_rgb` (bạn vẽ thêm `person`, khoảng 108×177 px và 178×181 px, trong `infant_seat`; mình chỉ vẽ `infant_seat`).
   Bạn tạm gán thế nào và vì sao: Ở S04 và S08 chỉ vẽ `infant_seat`, không vẽ `person`, theo GUIDE §3 (hình giống trẻ em thì báo coach, không gán). Ở S02, `export_final_v2.zip` đang ghi `occupied = no` kèm `person`; vì 4.8 chỉ cho `no` hoặc `unknown`, mình thấy `unknown` hợp lý hơn khi có người bên trong, và sẽ đổi nếu coach xác nhận.
2. Câu hỏi: Trên ảnh NIR thật (D##), đèn LED cận hồng ngoại luôn bật nên ảnh trông giống nhau ngày và đêm. Căn cứ nào để ghi `light = day` hoặc `night` thay vì `unknown`? Guideline chỉ liệt kê ba giá trị, không nói cách phân biệt trên NIR (4.4-1 chỉ nói không thấy thì `unknown`).
   Khung ví dụ: `D05` (`export_final_v2.zip`: `day`; bạn: `unknown`) và `D01` (v2: `night`; bạn: `unknown`). Trong v2, D01, D02, D03, D04, D06 là `night`, D05 là `day`; bản của bạn là `unknown` ở cả 6 ảnh.
   Bạn tạm gán thế nào và vì sao: Giữ như v2 vì đó là giá trị mình đã gán khi nhìn từng ảnh. Nếu coach cho biết NIR không đủ căn cứ để phân biệt ngày và đêm thì đổi cả 6 ảnh sang `unknown` theo 4.4-1.