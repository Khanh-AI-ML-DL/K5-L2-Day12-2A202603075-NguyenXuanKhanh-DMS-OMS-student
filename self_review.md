# Tự đánh giá — Nguyễn Xuân Khánh · G08

Căn cứ: `export_final.zip` (trước review), `export_final_v2.zip` (sau review), `Nguyen_final.zip` (bản của bạn ghép cặp), `check_final.txt`, `check_final_v2.txt` và Guideline Cabin v1.0.

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb / S01_ir | infant_seat | `seat_flip` | Box nằm ở nửa trái ảnh (x 144–376 trên ảnh rộng 960 px) nhưng mình gán `seat = rear_left`. Camera OMS nhìn về phía sau, nên trái ảnh là `rear_right` (4.4-3). Người ở nửa phải ảnh thì mình gán đúng `rear_left`. `cabin_check` không bắt được lỗi này, chỉ lộ ra khi `diff` với bạn (bạn gán `rear_right`). | **Chưa.** `export_final_v2.zip` vẫn còn `rear_left` |
| S02_rgb / S02_ir | child_seat | `missing` | Bản của bạn có thêm một `child_seat` ở nửa trái ảnh (`rear_right`, `occupied = no`), bản của mình không có. Cùng vị trí và kích thước (khoảng x 110–400, y 203–627) cũng xuất hiện ở S05 và S06 trong bản của bạn, và bản của mình cũng thiếu ở cả hai cảnh. Nhiều khả năng mình bỏ sót ghế trẻ em trống (4.2: ghế trẻ em trống phải có `child_seat`). | **Chưa.** v2 chưa thêm box. Cần mở lại S02, S05, S06 trên CVAT để xác nhận |
| D01.png | hand | `lr_flip` | Mình gán cả 2 tay của tài xế là `side = right`. `side` là trái/phải của chính người đó, mỗi người chỉ có 1 tay trái và 1 tay phải (4.7). `cabin_check` báo ERROR. | Đã sửa ở v2 (một tay đổi thành `left`) |
| D04.png | face, eye_left | `flag` | Mình để `eye_left = open` nhưng cả 4 điểm `left_eye_*` đều bị che. Không thấy mắt thì phải là `unknown` (4.4-1). | Đã sửa ở v2 (`eye_left = unknown`) |

Các lỗi cùng loại ở ảnh khác: S01 còn lỗi `guess` ở `light` (mình điền `day`, đúng ra là `unknown`, 4.1); D01 và D03 có mắt `unknown` nhưng điểm mắt không có cờ `occluded`/`outside`. Cả hai đã sửa ở v2.

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Điền `light` (`day` hoặc `night`) cho cả 16 ảnh SVIRO (S01 đến S08, bản `_rgb` và `_ir`), trong khi ảnh dựng thì `light` phải là `unknown` (Guideline 4.1, GUIDE 3). `check_final.txt` có 16 cảnh báo loại này, nhiều nhất trong các lỗi.

Vì sao mình mắc: Mình gán `light` theo cảm giác khi nhìn từng ảnh mà không áp luật riêng của ảnh dựng, rồi lặp lại cho các ảnh sau. Mình cũng chỉ chạy `cabin_check` sau khi đã gán xong cả 22 ảnh (checkpoint A và B chạy bù từ `export_final.zip`), nên lỗi không bị chặn từ S01 mà lặp 16 lần.

Lần sau tránh bằng cách: Xác định nguồn ảnh (SVIRO dựng hay Drive&Act thật) và đặt `light` trước khi vẽ box đầu tiên, đúng thứ tự ở 4.3. Export và chạy `cabin_check --only` ngay tại checkpoint, không chạy bù.

Lỗi thứ hai, nặng hơn về nội dung và chưa sửa: hai lỗi mà `cabin_check` không bắt được là gán ghế theo ảnh (S01) và thiếu `child_seat` (S02, S05, S06). Cách tránh: sau mỗi cảnh S##, đọc từng box theo thứ tự "trái ảnh, giữa, phải ảnh = rear_right, rear_middle, rear_left" rồi đếm ghế có vật so với số box. Ngoài ra ở S03_rgb, cả 3 box của mình lệch khoảng 20 px sang trái so với bản `_ir` cùng cảnh (và so với box của bạn). Cần kiểm lại vị trí box sau khi copy từ RGB sang IR (GUIDE §6, 4.4-5).

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: **S01, `infant_seat`, trường `seat`** (mình `rear_left`, bạn `rear_right`). Box nằm ở nửa trái ảnh nên theo 4.4-3 phải là `rear_right`. Mình học được: ghế phải gọi theo xe, không theo ảnh. Mình gán đúng người ở nửa phải ảnh là `rear_left` nhưng lại gán sai ghế em bé trong cùng một ảnh, nên cần kiểm từng box thay vì tin cả ảnh. Lỗi này vẫn còn trong `export_final_v2.zip`, ghi ở đây theo RULES 6.

Dòng thứ hai: **D01, `hand`, `side`** (mình `right`, bạn `left`). Bạn đúng vì `side` theo người và mỗi người chỉ có một tay mỗi bên. Đã sửa ở v2.

Hai dòng mình đúng, bạn sai, cần thống nhất lại với bạn: D03 `hand` (bạn gán cả 2 tay là `right`, trái 4.7) và S07 `person.seat` (bạn gán cả 2 người hàng sau là `driver`, trong khi họ ở `rear_left` và `rear_right`). Hai người trùng nhãn chỉ cho thấy nhất quán, chưa chắc đúng.